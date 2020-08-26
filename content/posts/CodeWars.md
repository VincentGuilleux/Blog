---
title: "CodeWars"
date: 2020-08-26T14:52:20+02:00
draft: false
tags: [Algorithmique]
---

Pour progresser en algorithmique, je fais de temps en temps des [exercices](https://github.com/VincentGuilleux/codewars) sur [CodeWars](https://www.codewars.com/).

Je vais partager aujourd'hui mon raisonnement sur un [problème](https://www.codewars.com/kata/51b6249c4612257ac0000005) que j'avais trouvé intéressant : la conversion d'un nombre en chiffres romains vers sa valeur dans notre système décimal. La fonction correspondante est nommée conversion et prend pour unique paramètre la chaîne de caractères correspondant au nombre libellé en chiffre romains.

```ruby
def conversion(roman)
end
```

Avec un exemple de possible test booléen associé :
```ruby
pp conversion('MCMXC') == 1990
```

Si on reformule ce problème en pseudo-code, il nous faut :
1. Associer à chaque lettre en chiffres romains sa contre-valeur en nombre entier.
2. Décomposer la chaîne de caractères de l'input en un array composé de chacun des caractères.
3. Itérer sur ces caractères en chiffres romains ; pour chacun :\
  3.1. Si la lettre suivante est d'une valeur supérieure (ou s'il n'y pas de lettre suivante), ajouter au résultat la valeur de la lettre en cours.\
  3.2. Si la lettre suivante est d'une valeur inférieure, ajouter au résultat la différence entre la valeur de la lettre suivante et celle de la lettre en cours. Dans ce cas, à la prochaine itération, repartir de la lettre juste après la ligne suivante.


Voilà, le plus dur est fait :) Reste juste à traduire le tout sous forme de Code Ruby, ce qui donne :\
1.
```ruby
conv_table = {
      'I' => 1,
      'V' => 5,
      'X' => 10,
      'L' => 50,
      'C' => 100,
      'D' => 500,
      'M' => 1000
}
```
2.
```ruby
roman_array = roman.chars
result = 0
```
3.
```ruby
i = 0
until i == roman.length
  current_letter_value = conv_table[roman_array[i]]
  next_letter_value = conv_table[roman_array[i + 1]]
  if next_letter_value.nil? || current_letter_value >= next_letter_value
    result += current_letter_value
  else
    result += (next_letter_value - current_letter_value)
    i += 1
  end
    i += 1
end
```

Voilà une première version de la fonction de conversion valide. Après refactorisation et utilisation de l'itérateur *each*, cette même solution peut être synthétisée comme suit :
```ruby
def conversion_refacto(roman)
  result = 0
  conv_table = {
    'I' => 1,
    'V' => 5,
    'X' => 10,
    'L' => 50,
    'C' => 100,
    'D' => 500,
    'M' => 1000
  }

  roman.chars.each_with_index do |char, index|
    current_letter_value = conv_table[char]
    next_letter_value = conv_table[roman.chars[index + 1]]
    next_letter_value.nil? || current_letter_value >= next_letter_value ? result += current_letter_value : result -= current_letter_value
  end
  result
end
```

Il est possible de faire syntaxiquement encore plus court. C'est un des intérêts de CodeWars, dès que nous soumettons une solution valide, cela donne accès à toutes les autres solutions correctes soumises par les autres utilisateurs et celles-ci sont classées par pertinence.

Ci-dessous donc une autre solution valable parmi les mieux notées sur le site :

```ruby
def conversion(roman)
  conv_table = {
    'M' => 1000,
    'D' => 500,
    'C' => 100,
    'L' => 50,
    'X' => 10,
    'V' => 5,
    'I' => 1,
  }

  digits = roman.chars.reverse.map{|d| conv_table[d]}
  digits.map.with_index { |d, i| digits[i.zero? ? i : i - 1] > d ? -d : d }.reduce(:+)
end
```

La première ligne digits renvoit :
  * un array en sens inverse de chacun des caractères de l'input : *roman.chars.reverse*
  * mappé vers sa valeur en système décimal : *.map{ |d| conv_table[d] }*\
=> Pour notre test avec ''MCMXC', cela renverra par exemple : [100, 10, 1000, 100, 1000]

La dernière ligne digits renvoit pour chaque membre de l'array digits de valeur d et d'index i : *digits.map.with_index { |d, i|  ... }*
  * sa valeur pour l'index i-1 (sauf pour l'index 0 qui renvoit la valeur de l'index 0) : *digits.map.with_index {|d, i| digits[i.zero? ? i : i - 1]}*\
  => Soit dans notre exemple : [[100], [100], [10], [1000], [100]]
  * la valeur renvoyée ci-dessus est ensuite comparée à la valeur de l'index i : si strictement supérieure, l'entier est renvoyé en négatif, sinon en positif : *digits[i.zero? ? i : i - 1] > d ? -d : d}*\
  Autrement dit, pour chaque couple d'index [i-1, i], si la valeur de l'index i-1 est supérieure à la valeur d de l'index i, il convient de soustraire la valeur de l'index i et de l'additionner dans le cas contraire. On retrouve ici la logique de la solution proposée plus haut.\
  => Soit dans notre exemple : [100, -10, 1000, -100, 1000]
  * ne reste alors plus qu'à sommer toutes les valeurs de l'array ainsi généré :
  *.reduce(:+)*

NB : pour ceux qui comme moi se posent la question de l'intérêt dans cette solution de *reverse* l'array, testez la sans le *reverse* avec par exemple 'XXI'.

En conclusion, je trouve très utile d'avoir accès aux solutions notées les plus pertinentes afin d'améliorer sa syntaxe et sa logique algorithmique. Cela dit, dans certains cas, à mon niveau, la volonté de compression syntaxique peut prendre le pas sur la lisibilité et la compréhension du code :)
