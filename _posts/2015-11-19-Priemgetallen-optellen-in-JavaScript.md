---
layout: post
title: Priemgetallen optellen in JavaScript
---

Een interessante oefening gisteren op [FreeCodeCamp](http://www.freecodecamp.com): ontwerp een functie die alle priemgetallen optelt die lager zijn dan een opgegeven getal.

Het duurde niet lang voor ik een werkende oplossing had:

```
function sumPrimes(num) {

  var result = 2;  //starting value of 2 because that is the lowest prime number (which will therefore always be included, unless num == 1)
  var currentNumber = 3;  //the for loop has to start at 3 because result has the starting value 2.
  var divider = 2;
  
  // 1 is not a prime, so return nothing. Also stops the for loop from happening.
  if (num === 1){
    return 0;
  }
  
  //looping through every number from 3 until num
  for (currentNumber = 3; currentNumber <= num; currentNumber++) {
    //divide currentNumber by all lower numbers (except 1) to check if currentNumber is a prime
    for (divider = 2; divider <= currentNumber; divider++) {
      if (currentNumber % divider === 0) {
        break;
      }
    }
    if (currentNumber == divider) {
      result += currentNumber;
    }
  }
  
  return result;
}
```

Ik ben best wel trots dat ik een oplossing gevonden heb waarvoor je geen `array` nodig hebt. Het leek mij onelegant om alle gevonden priemgetallen in een array te zetten en dan pas op te tellen. Dit heeft een spijtig nadeel (zie verder), maar eerst zijn hier een paar elementen waarmee ik een beetje worstelde:
* De startwaarden van de verschillende variabelen. In tegenstelling tot de meeste `for`-loops, begin je hier niet bij nul. Twee is het eerste priemgetal, maar `divider` kan niet 1 als startwaarde hebben (dan zou 1 zelf ook als priemgetal gedetecteerd worden). Daarom begint `currentNumber` met startwaarde 3 en `divider` met 2.
* Oorspronkelijk had ik de lijn `result += currentNumber` binnen de `divider`-loop gezet. Dit had natuurlijk tot gevolg dat `currentNumber` aan `result` werd toegevoegd telkens het niet deelbaar was door `divider`. Het optellen moest dus buiten die loop, maar het heeft nog even geduurd voor ik de juiste formulering had gevonden voor de voorwaarde. Hoe kom ik te weten of currentNumber een priemgetal is na het einde van de `divider`-loop? Eenvoudig: als `currentNumber == divider`.

Mijn oplossing heeft zoals gezegd een groot nadeel. Bij elke iteratie doorloopt `divider` opnieuw alle natuurlijke getallen die kleiner zijn dan `currentNumber`. Voor de opgave was dit niet zo'n probleem: FreeCodeCamp test de code alleen met relatief kleine getallen. Het is echter veel efficiënter om enkel te delen door priemgetallen in plaats van alle natuurlijke getallen. Dit zorgt uiteraard ook voor veel minder vertraging als je dit probeert met echt grote getallen. In mijn code lukt dit echter niet zomaar. Om dit te kunnen doen heb je een array nodig die voor elk getal (kleiner dan het opgegeven getal) bijhoudt of het al dan niet een priemgetal is. Ik heb tenminste nog geen manier gevonden om het zonder te doen. Voorlopig laat ik het zoals het is, maar misschien keer ik later terug naar deze opgave om dit probleem op te lossen.

De opgave is [hier](http://www.freecodecamp.com/challenges/bonfire-sum-all-primes) te vinden.