<h1>Zadanie 2</h1>
Dane dotyczą kodów pocztowych w Polsce

Przygotowanie pliku ze strony http://piotr.eldora.pl/bazy-danych-kody-pocztowe-imiona-panstwa za pomoca google refine.

<h2>MongoDB<h2>

import danych do mongodb odbyl sie za pomoca

```
mongoimport --db kody --collection kody --fields id,kod-pocztowy,poczta,wojewodztwo,ulica,powiat,numery,gmina --headerline --type csv --file kody.csv
```

Agregacje

```
db.kody.aggregate({$group: {_id:"$poczta", suma_kodow:{$sum:1}} }, {$sort: {suma_kodow:-1} }, {$limit:10})
```

```
{
	"result" : [
		{
			"_id" : "szczecin",
			"suma_kodow" : 4157
		},
		{
			"_id" : "gdańsk",
			"suma_kodow" : 1829
		},
...
}
```


```
db.kody.aggregate({$group: {_id:"$powiat", suma_kodow:{$sum:1}} }, {$sort: {suma_kodow:-1} }, {$limit:10})
```

```
{
	"result" : [
		{
			"_id" : "m. st. warszawa",
			"suma_kodow" : 7793
		},
		{
			"_id" : "m. szczecin",
			"suma_kodow" : 4153
		},
...
}
```



