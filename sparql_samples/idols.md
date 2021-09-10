# アイドル一覧　(SPARQLのサンプル)

## シンデレラガールズ

```sparql
PREFIX schema: <http://schema.org/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX imas: <https://sparql.crssnky.xyz/imasrdf/URIs/imas-schema.ttl#>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
SELECT 
    ?label
	(max(coalesce(if(lang(?ofname)="ja",str(?ofname),""),"")) as ?fname_ja)
	(max(coalesce(if(lang(?ogname)="ja",str(?ogname),""),"")) as ?gname_ja)
	(max(coalesce(if(lang(?ofnamekana)="ja",str(?ofnamekana),""),"")) as ?fnamekana)
	(max(coalesce(if(lang(?ognamekana)="ja",str(?ognamekana),""),"")) as ?gnamekana)
	(max(coalesce(if(lang(?ofname)="en",str(?ofname),""),"")) as ?fname_en)
	(max(coalesce(if(lang(?ogname)="en",str(?ogname),""),"")) as ?gname_en)
	(max(str(?oheight)) as ?height)
	(max(str(?oweight)) as ?weight)
	(max(str(?obust)) as ?bust)
	(max(str(?owaist)) as ?waist)
	(max(str(?ohip)) as ?hip)
	(max(str(?oblood)) as ?blood)
	(max(str(?oage)) as ?age)
	(max(str(?obirthdate)) as ?birthdate)
	(max(str(?obirthplace)) as ?birthplace)
	(max(coalesce(if(lang(?oconste)="ja",str(?oconste),""),"")) as ?conste_ja)
	(replace(replace(group_concat(distinct coalesce(if(lang(?ohobby)="ja",?ohobby, ""), ""); separator=" "), "  ", " "), "^ | $", "") as ?hobby_ja)
	(max(str(?otype)) as ?type)
	(replace(replace(group_concat(distinct coalesce(if(lang(?opoplinkattr)="ja",?opoplinkattr, ""), ""); separator=" "), "  ", " "), "^ | $", "") as ?poplinkattr_ja)
	(replace(replace(group_concat(distinct coalesce(if(lang(?opoplinkattr)="en",?opoplinkattr, ""), ""); separator=" "), "  ", " "), "^ | $", "") as ?poplinkattr_en)
	(max(coalesce(if(lang(?ocv)="ja",str(?ocv),""),"")) as ?cv_ja)
	(max(str(?ocolor)) as ?color)
WHERE { SELECT
    ?s ?label
    ?ofname ?ogname ?ofnamekana ?ognamekana
	?oconste ?ocv ?opoplinkattr ?otype ?oheight ?oweight ?obust ?owaist ?ohip ?ocolor
	?oage ?obirthdate ?obirthplace ?oblood ?ohobby
  WHERE {
    ?s rdfs:label ?label ;
       rdf:type <https://sparql.crssnky.xyz/imasrdf/URIs/imas-schema.ttl#Idol>;
       imas:Brand "CinderellaGirls"@en .
	   OPTIONAL {?s schema:familyName ?ofname}
	   OPTIONAL {?s schema:givenName ?ogname}
	   OPTIONAL {?s imas:familyNameKana ?ofnamekana}
	   OPTIONAL {?s imas:givenNameKana ?ognamekana}
       OPTIONAL {?s imas:Constellation ?oconste}
       OPTIONAL {?s imas:cv ?ocv}
	   OPTIONAL {?s imas:PopLinksAttribute ?opoplinkattr}
	   OPTIONAL {?s imas:Type ?otype}
	   OPTIONAL {?s schema:height ?oheight}
	   OPTIONAL {?s schema:weight ?oweight}
	   OPTIONAL {?s imas:Bust ?obust}
	   OPTIONAL {?s imas:Waist ?owaist}
	   OPTIONAL {?s imas:Hip ?ohip}
	   OPTIONAL {?s imas:Color ?ocolor}
	   OPTIONAL {?s foaf:age ?oage}
	   OPTIONAL {?s schema:birthDate ?obirthdate}
	   OPTIONAL {?s schema:birthPlace ?obirthplace}
	   OPTIONAL {?s imas:BloodType ?oblood}
	   OPTIONAL {?s imas:Hobby ?ohobby}
  }
  ORDER BY ?s ?opoplinkattr ?ohobby
}
GROUP BY ?s ?label
ORDER BY ?fnamekana ?gnamekana
```
