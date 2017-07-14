---
layout: page
title: Sample queries
permalink: /queries/
---

# [1. Biotea + Reactome + COLIL](#1-biotea--reactome--colil-1)

# [2. Biotea + Uniprot](#2-biotea--uniprot-1)

# [3. Annotations coming from GO or CHEBI in articles with snomed:Renal cell carcinoma](#3-annotations-coming-from-go-or-chebi-in-articles-with-snomedrenal-cell-carcinoma-1)

# [4. Common SNOMED CT tags between two articles (pmc:3875424 and pmc:3933681)](#4-common-snomed-ct-tags-between-two-articles-pmc3875424-and-pmc3933681-1)

# [5. Get all the annotations for one article (pmc:3865095)](#5-get-all-the-annotations-for-one-article-pmc3865095-1)

# [6. Biotea + Uniprot + DBPedia](#6-biotea--uniprot--dbpedia-1)

# [7. Biotea + Open Citations](#7-biotea--open-citations-1)

## 1. Biotea + Reactome + COLIL

Retrieve all the pathways referencing “insulin” from Reactome and also search for the literature annotated with GO terms like “chemical homeostasis” or any of its subclasses, e.g. “lipid homeostasis” and “triglyceride catabolic process”, the NCIt “insulin” and “insulin signaling pathway” as well as the SNOMED term “homeostasis” -all of these are GO annotations in the resulting pathways from Reactome along with the citations contexts of the papers coming from COLIL.

<a href="http%3A%2F%2Fbiotea.linkeddata.es%2Fsparql%3Fdefault-graph-uri%3D%26query%3DPREFIX%20rdfs%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0APREFIX%20xsd%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0APREFIX%20oa%3A%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E%0APREFIX%20biotea%3A%3Chttps%3A%2F%2Fbiotea.github.io%2Fbiotea-ontololgy%23%3E%0APREFIX%20dcterms%3A%20%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0APREFIX%20rdf%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0APREFIX%20owl%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2002%2F07%2Fowl%23%3E%0APREFIX%20bibo%3A%20%3Chttp%3A%2F%2Fpurl.org%2Fontology%2Fbibo%2F%3E%0APREFIX%20colil%3A%20%3Chttp%3A%2F%2Fpurl.jp%2Fbio%2F10%2Fcolil%2Fontology%2F201303%23%3E%0APREFIX%20doco%3A%20%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Fdoco%2F%3E%0APREFIX%20togows%3A%20%3Chttp%3A%2F%2Ftogows.dbcls.jp%2Fontology%2Fncbi-pubmed%23%3E%0APREFIX%20biopax3%3A%20%3Chttp%3A%2F%2Fwww.biopax.org%2Frelease%2Fbiopax-level3.owl%23%3E%0A%0ASELECT%20DISTINCT%20%3FarticleTitle%20%3Fpmid%20(GROUP_CONCAT(DISTINCT(%3Fcontext)%3Bseparator%3D%22%7C%22)%20as%20%3Fcontexts)%20(GROUP_CONCAT(DISTINCT(%3Fpathwayname)%3Bseparator%3D%22%7C%22)%20as%20%3Fpathwaynames)%0AWHERE%20%7B%0A%0A%09%3FannotInsulin%20a%20oa%3AAnnotation%20%3B%0A%09%09%20%20oa%3AhasTarget%20%3FparagraphInsulin%20%3B%0A%09%09%20%20oa%3AhasBody%20%3Chttp%3A%2F%2Fpurl.bioontology.org%2Fontology%2FSNOMEDCT%2F21979002%3E.%0A%09%3FparagraphInsulin%20oa%3AhasSource%20%3Farticle%20.%0A%09%3Farticle%20dcterms%3Atitle%20%3FarticleTitle%20.%0A%20%20%20%20%20%20%20%20%3Farticle%20bibo%3Apmid%20%3Fpmid%20.%0A%20%20%20%20%7B%0A%09SERVICE%20%3Chttp%3A%2F%2Fsparql.bioontology.org%2Fontologies%2Fsparql%2F%3Fapikey%3DINSERT%20YOUR%20API%20KEY%20HERE%3E%20%7B%0A%09%09%3Fchild%20rdfs%3AsubClassOf%20%3Chttp%3A%2F%2Fpurl.obolibrary.org%2Fobo%2FGO_0048878%3E%20.%0A%09%7D%0A%20%20%20%20%20%20%20%20%3Fparagraph%20oa%3AhasSource%20%3Farticle%20.%0A%20%20%20%20%20%20%20%20%3Fannot%20a%20oa%3AAnnotation%20%3B%0A%09%09%20%20oa%3AhasTarget%20%3Fparagraph%20%3B%0A%09%09%20%20oa%3AhasBody%20%3FannotationBody.%0A%20%20%20%20%20%20%20FILTER(%3FannotationBody%20IN%20(%3Fchild%2C%20%3Chttp%3A%2F%2Fpurl.obolibrary.org%2Fobo%2FGO_0048878%3E%2C%20%3Chttp%3A%2F%2Fncicb.nci.nih.gov%2Fxml%2Fowl%2FEVS%2FThesaurus.owl%23C2271%3E))%0A%20%20%20%20%7D%0A%20%20%20%20SERVICE%20%3Chttp%3A%2F%2Fcolil.dbcls.jp%2Fsparql%3E%20%7B%0A%09%09%3FcitationPaper%20bibo%3Acites%20%3FreferencePaper%20.%0A%09%09%3FcitationPaper%20doco%3Acontains%20%5B%0A%09%09%20%20doco%3Acontains%20%5B%0A%09%09%20%20%20%20rdf%3Avalue%20%3Fcontext%20%3B%0A%09%09%20%20%20%20colil%3Amentions%20%3FreferencePaper%0A%09%09%20%20%5D%0A%09%09%5D%20.%0A%09%09%3FreferencePaper%20rdfs%3AseeAlso%20%5B%0A%09%09%20%20rdf%3Atype%20colil%3APubMed%20%3B%0A%09%09%20%20togows%3Apmid%20%3Fpmid%0A%09%09%5D%20.%0A%09%7D%0A%09SERVICE%20%3Chttps%3A%2F%2Fwww.ebi.ac.uk%2Frdf%2Fservices%2Freactome%2Fsparql%3E%20%7B%0A%09%09%3Fpathway%20rdf%3Atype%20biopax3%3APathway%20.%0A%09%09%3Fpathway%20biopax3%3AdisplayName%20%3Fpathwayname%20.%0A%09%09%3Fpathway%20biopax3%3ApathwayComponent%20%3Freaction%20.%20%0A%09%09%3Freaction%20rdf%3Atype%20biopax3%3ABiochemicalReaction%20.%20%0A%09%09%7B%0A%09%09%09%7B%3Freaction%20%3Frel%20%3Fprotein%20.%7D%20%20%20%0A%09%20%20%20%09%09UNION%20%0A%09%20%20%20%09%09%7B%0A%09%20%20%20%09%09%09%3Freaction%20%20%3Frel%20%20%3Fcomplex%20.%20%0A%09%09%09%09%3Fcomplex%20rdf%3Atype%20biopax3%3AComplex%20.%20%20%0A%09%09%09%09%3Fcomplex%20%3Fcomp%20%3Fprotein%20.%20%0A%09%09%09%7D%0A%09%09%7D%20%0A%09%09%3Fprotein%20rdf%3Atype%20biopax3%3AProtein%20.%20%0A%09%09%3Fprotein%20biopax3%3AentityReference%20%3Chttp%3A%2F%2Fpurl.uniprot.org%2Funiprot%2FP01308%3E%20%0A%09%7D%20%0A%7D%20GROUP%20BY%20%3FarticleTitle%20%3Fpmid%0A%26should-sponge%3D%26format%3Dtext%2Fhtml%26timeout%3D300000%26debug%3Don" target="_blank">Execute it in the endpoint</a>

```
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX oa:<http://www.w3.org/ns/oa#>
PREFIX biotea:<https://biotea.github.io/biotea-ontololgy#>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX bibo: <http://purl.org/ontology/bibo/>
PREFIX colil: <http://purl.jp/bio/10/colil/ontology/201303#>
PREFIX doco: <http://purl.org/spar/doco/>
PREFIX togows: <http://togows.dbcls.jp/ontology/ncbi-pubmed#>
PREFIX biopax3: <http://www.biopax.org/release/biopax-level3.owl#>

SELECT DISTINCT ?articleTitle ?pmid (GROUP_CONCAT(DISTINCT(?context);separator="|") as ?contexts) (GROUP_CONCAT(DISTINCT(?pathwayname);separator="|") as ?pathwaynames)
WHERE {

	?annotInsulin a oa:Annotation ;
		  oa:hasTarget ?paragraphInsulin ;
		  oa:hasBody <http://purl.bioontology.org/ontology/SNOMEDCT/21979002>.
	?paragraphInsulin oa:hasSource ?article .
	?article dcterms:title ?articleTitle .
        ?article bibo:pmid ?pmid .
    {
	SERVICE <http://sparql.bioontology.org/ontologies/sparql/?apikey=INSERT YOUR API KEY HERE> {
		?child rdfs:subClassOf <http://purl.obolibrary.org/obo/GO_0048878> .
	}
        ?paragraph oa:hasSource ?article .
        ?annot a oa:Annotation ;
		  oa:hasTarget ?paragraph ;
		  oa:hasBody ?annotationBody.
       FILTER(?annotationBody IN (?child, <http://purl.obolibrary.org/obo/GO_0048878>, <http://ncicb.nci.nih.gov/xml/owl/EVS/Thesaurus.owl#C2271>))
    }
    SERVICE <http://colil.dbcls.jp/sparql> {
		?citationPaper bibo:cites ?referencePaper .
		?citationPaper doco:contains [
		  doco:contains [
		    rdf:value ?context ;
		    colil:mentions ?referencePaper
		  ]
		] .
		?referencePaper rdfs:seeAlso [
		  rdf:type colil:PubMed ;
		  togows:pmid ?pmid
		] .
	}
	SERVICE <https://www.ebi.ac.uk/rdf/services/reactome/sparql> {
		?pathway rdf:type biopax3:Pathway .
		?pathway biopax3:displayName ?pathwayname .
		?pathway biopax3:pathwayComponent ?reaction . 
		?reaction rdf:type biopax3:BiochemicalReaction . 
		{
			{?reaction ?rel ?protein .}   
	   		UNION 
	   		{
	   			?reaction  ?rel  ?complex . 
				?complex rdf:type biopax3:Complex .  
				?complex ?comp ?protein . 
			}
		} 
		?protein rdf:type biopax3:Protein . 
		?protein biopax3:entityReference <http://purl.uniprot.org/uniprot/P01308> 
	} 
} GROUP BY ?articleTitle ?pmid

```


## 2. Biotea + Uniprot

Retrieve all the articles containing ncit:Placebo Control, ncit:Crossover Study, snomed:Glucose tolerance test, go:insulin secretion, go:glucose metabolic process and the entries from Uniprot related with go:glucose metabolic process, go:response to insulin and uniprot:Diabetes mellitus, non-insulin-dependent (NIDDM).


<a href="http://smartprotocols.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+sp%3A+%3Chttp%3A%2F%2Fpurl.org%2Fnet%2FSMARTprotocol%23%3E%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+ro%3A+%3Chttp%3A%2F%2Fwww.obofoundry.org%2Fro%2Fro.owl%23%3E%0D%0APREFIX+owl%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2002%2F07%2Fowl%23%3E%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+dbo%3A+%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0A%0D%0ASELECT+%3Ftitle+%3FspecimenName%0D%0AWHERE+%7B%0D%0A++%3Fprotocol+sp%3AhasTitle+%3Ftitle_uri+.%0D%0A++%3Ftitle_uri+rdf%3Avalue+%3Ftitle+.%0D%0A++%3Fprotocol+sp%3AhasExperimentalInput+%3Fspecimens+.%0D%0A++%3Fspecimens+a+sp%3ASpecimenList+.%0D%0A++%3Fspecimens+ro%3Ahas_part+%3FspecimenNameUri.%0D%0A++%3FspecimenNameUri+rdf%3Avalue+%3FspecimenName+.%0D%0A++%3Fspecimen+sp%3AhasName+%3FspecimenNameUri.%0D%0A++SERVICE+%3Chttps%3A%2F%2Fdbpedia.org%2Fsparql%3E%0D%0A++%7B%0D%0A++++%3FexternalUri+dbo%3Aorder+%3Chttp%3A%2F%2Fdbpedia.org%2Fresource%2FRodent%3E+.%0D%0A++++%3FexternalUri+rdfs%3Acomment+%3FdbpediaDesc+.%0D%0A++++FILTER%28lang%28%3FdbpediaDesc%29+%3D+%27en%27%29%0D%0A++%7D%0D%0A++%3Fspecimen+owl%3AsameAs+%3FexternalUri+.%0D%0A%7D&should-sponge=&format=text%2Fhtml&timeout=0&debug=on" target="_blank">Execute it in the endpoint</a>

```
PREFIX uniprotkb:<http://purl.uniprot.org/core/> 
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX oa:<http://www.w3.org/ns/oa#>
PREFIX biotea:<https://biotea.github.io/biotea-ontololgy#>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX bibo: <http://purl.org/ontology/bibo/>

select distinct ?articleTitle ?pmid (GROUP_CONCAT(?uniprotEntry;separator="|") as ?uniprotEntries) where {

		?placeboAnnot a oa:Annotation ;
		  oa:hasTarget ?placeboParagraph ;
		  oa:hasBody <http://ncicb.nci.nih.gov/xml/owl/EVS/Thesaurus.owl#C49648> .
		?placeboParagraph oa:hasSource ?article .

		?crossoverAnnot a oa:Annotation ;
		  oa:hasTarget ?crossoverParagraph ;
		  oa:hasBody <http://ncicb.nci.nih.gov/xml/owl/EVS/Thesaurus.owl#C82637> .
		?crossoverParagraph oa:hasSource ?article .

		?glucoseAnnot a oa:Annotation ;
		  oa:hasTarget ?glucoseParagraph ;
		  oa:hasBody <http://purl.bioontology.org/ontology/SNOMEDCT/113076002> .
		?glucoseParagraph oa:hasSource ?article .

		?insulinAnnot a oa:Annotation ;
		  oa:hasTarget ?insulinParagraph ;
		  oa:hasBody <http://purl.obolibrary.org/obo/GO_0030073> .
		?insulinParagraph oa:hasSource ?article .

		?metabolicAnnot a oa:Annotation ;
		  oa:hasTarget ?metabolicParagraph ;
		  oa:hasBody <http://purl.obolibrary.org/obo/GO_0006006> .
		?metabolicParagraph oa:hasSource ?article .

		?article dcterms:title ?articleTitle .
        ?article bibo:pmid ?pmid .

	SERVICE <http://sparql.uniprot.org/sparql> {
		 ?uniprotEntry uniprotkb:classifiedWith <http://purl.obolibrary.org/obo/GO_0006006> .
		 ?uniprotEntry uniprotkb:classifiedWith <http://purl.obolibrary.org/obo/GO_0032868> .
		 ?unitprotEntry uniprotkb:annotation ?uniprotEntryAnnotation .
		 ?uniprotEntryAnnotation uniprotkb:disease <http://purl.uniprot.org/diseases/2060> .
		}
} GROUP BY ?articleTitle ?pmid
```

## 3. Annotations coming from GO or CHEBI in articles with snomed:Renal cell carcinoma
<a href="http://biotea.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+xsd%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0D%0APREFIX+oa%3A%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E%0D%0APREFIX+biotea%3A%3Chttps%3A%2F%2Fbiotea.github.io%2Fbiotea-ontololgy%23%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Farticle+%3Fannot+STR%28%3FstrText%29+AS+%3Ftext+xsd%3Ainteger%28%3Ftf%29+AS+%3Ffrequency+%3FontoBody+%0D%0AWHERE+%7B%0D%0A++SELECT+DISTINCT+%3Farticle+%3Fannot+%3FstrText+%3Ftf+%3FontoBody+%0D%0A++WHERE+%7B%0D%0A++++%3Fannot+a+oa%3AAnnotation+%3B%0D%0A++++++oa%3AhasTarget+%3Fparagraph+%3B%0D%0A++++++oa%3AhasBody+%3FontoBody+%3B%0D%0A++++++oa%3AhasBody+%3FtextualBody+%3B%0D%0A++++++biotea%3Atf+%3Ftf+.%0D%0A++++%3Fparagraph+oa%3AhasSource+%3Farticle+.%0D%0A++++%3FtextualBody+a+oa%3ATextualBody+%3B%0D%0A++++++rdf%3Avalue+%3FstrText+.%0D%0A++++FILTER+%28STRSTARTS%28STR%28%3FontoBody%29%2C+%22http%3A%2F%2Fpurl.obolibrary.org%2Fobo%2FGO_%22%29+%7C%7C+STRSTARTS%28STR%28%3FontoBody%29%2C+%22http%3A%2F%2Fpurl.obolibrary.org%2Fobo%2FCHEBI_%22%29%29%0D%0A++++%7B%0D%0A++++++SELECT+DISTINCT+%3Farticle%0D%0A++++++WHERE+%7B%0D%0A++++++++%3Fannot+a+oa%3AAnnotation+%3B%0D%0A++++++++++oa%3AhasTarget+%3Fparagraph+%3B%0D%0A++++++++++oa%3AhasBody+%3Chttp%3A%2F%2Fpurl.bioontology.org%2Fontology%2FSNOMEDCT%2F41607009%3E+.%0D%0A++++++++%3Fparagraph+oa%3AhasSource+%3Farticle+.%0D%0A++++++%7D%0D%0A++++%7D%0D%0A++%7D+ORDER+BY+%3Farticle+%3Fannot+%3FontoBody%0D%0A%7D&should-sponge=&format=text%2Fhtml&timeout=300000&debug=on" target="_blank">Execute it in the endpoint</a>
```
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX oa:<http://www.w3.org/ns/oa#>
PREFIX biotea:<https://biotea.github.io/biotea-ontololgy#>

SELECT DISTINCT ?article ?annot STR(?strText) AS ?text xsd:integer(?tf) AS ?frequency ?ontoBody 
WHERE {
  SELECT DISTINCT ?article ?annot ?strText ?tf ?ontoBody 
  WHERE {
    ?annot a oa:Annotation ;
      oa:hasTarget ?paragraph ;
      oa:hasBody ?ontoBody ;
      oa:hasBody ?textualBody ;
      biotea:tf ?tf .
    ?paragraph oa:hasSource ?article .
    ?textualBody a oa:TextualBody ;
      rdf:value ?strText .
    FILTER (STRSTARTS(STR(?ontoBody), "http://purl.obolibrary.org/obo/GO_") || STRSTARTS(STR(?ontoBody), "http://purl.obolibrary.org/obo/CHEBI_"))
    {
      SELECT DISTINCT ?article
      WHERE {
        ?annot a oa:Annotation ;
          oa:hasTarget ?paragraph ;
          oa:hasBody <http://purl.bioontology.org/ontology/SNOMEDCT/41607009> .
        ?paragraph oa:hasSource ?article .
      }
    }
  } ORDER BY ?article ?annot ?ontoBody
}

```

## 4. Common SNOMED CT tags between two articles (pmc:3875424 and pmc:3933681)
<a href="http://biotea.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+oa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E%0D%0APREFIX+biotea%3A+%3Chttps%3A%2F%2Fbiotea.github.io%2Fbiotea-ontololgy%23%3E%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0A%0D%0ASELECT+DISTINCT+%3FtermUri+%3FtermFrequency+%3FtermFrequency1+%3Flabel%0D%0A%7B%0D%0A++++%3Fannotation+a+oa%3AAnnotation+.%0D%0A++++%3Fannotation+oa%3AhasTarget+%3Fparagraph+.%0D%0A++++%3Fannotation+oa%3AhasBody+%3FtermUri+.%0D%0A++++%3Fannotation+oa%3AhasBody+%3Ftext+.%0D%0A++++%3Ftext+rdf%3Avalue+%3Flabel+.%0D%0A++++%3Fannotation+biotea%3Atf+%3FtermFrequency+.%0D%0A++++%3Fparagraph+oa%3AhasSource+%3Chttp%3A%2F%2Flinkingdata.io%2Fpmcdoc%2Fpmc%2F3875424%3E+.%0D%0A++++%0D%0A++++%3Fannotation1+a+oa%3AAnnotation+.%0D%0A++++%3Fannotation1+oa%3AhasTarget+%3Fparagraph1+.%0D%0A++++%3Fannotation1+oa%3AhasBody+%3FtermUri+.%0D%0A++++%3Fannotation1+oa%3AhasBody+%3Ftext1+.%0D%0A++++%3Ftext1+rdf%3Avalue+%3Flabel1+.%0D%0A++++%3Fannotation1+biotea%3Atf+%3FtermFrequency1+.%0D%0A++++%3Fparagraph1+oa%3AhasSource+%3Chttp%3A%2F%2Flinkingdata.io%2Fpmcdoc%2Fpmc%2F3933681%3E+.%0D%0A%0D%0A++++FILTER+NOT+EXISTS+%7B+%3FtermUri+a+oa%3ATextualBody+%7D%0D%0A++++FILTER+%28+STRSTARTS%28STR%28%3FtermUri%29%2C+%22http%3A%2F%2Fpurl.bioontology.org%2Fontology%2FSNOMEDCT%22%29+%29%0D%0A%7D%0D%0A&should-sponge=&format=text%2Fhtml&timeout=300000&debug=on" target="_blank">Execute it in the endpoint</a>
```
PREFIX oa: <http://www.w3.org/ns/oa#>
PREFIX biotea: <https://biotea.github.io/biotea-ontololgy#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?termUri ?termFrequency ?termFrequency1 ?label
{
    ?annotation a oa:Annotation .
    ?annotation oa:hasTarget ?paragraph .
    ?annotation oa:hasBody ?termUri .
    ?annotation oa:hasBody ?text .
    ?text rdf:value ?label .
    ?annotation biotea:tf ?termFrequency .
    ?paragraph oa:hasSource <http://linkingdata.io/pmcdoc/pmc/3875424> .
    
    ?annotation1 a oa:Annotation .
    ?annotation1 oa:hasTarget ?paragraph1 .
    ?annotation1 oa:hasBody ?termUri .
    ?annotation1 oa:hasBody ?text1 .
    ?text1 rdf:value ?label1 .
    ?annotation1 biotea:tf ?termFrequency1 .
    ?paragraph1 oa:hasSource <http://linkingdata.io/pmcdoc/pmc/3933681> .

    FILTER NOT EXISTS { ?termUri a oa:TextualBody }
    FILTER ( STRSTARTS(STR(?termUri), "http://purl.bioontology.org/ontology/SNOMEDCT") )
}

```

## 5. Get all the annotations for one article (pmc:3865095)
<a href="http://biotea.linkeddata.es/sparql?default-graph-uri=&query=%0D%0APREFIX+oa%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E%0D%0APREFIX+biotea%3A+%3Chttps%3A%2F%2Fbiotea.github.io%2Fbiotea-ontololgy%23%3E%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0A%0D%0ASELECT+DISTINCT+%3FtermUri+%3FtermFrequency+%3Flabel%0D%0A%7B%0D%0A++++%3Fannotation+a+oa%3AAnnotation+.%0D%0A++++%3Fannotation+oa%3AhasTarget+%3Fparagraph+.%0D%0A++++%3Fannotation+oa%3AhasBody+%3FtermUri+.%0D%0A++++%3Fannotation+oa%3AhasBody+%3Ftext+.%0D%0A++++%3Ftext+rdf%3Avalue+%3Flabel+.%0D%0A++++%3Fannotation+biotea%3Atf+%3FtermFrequency+.%0D%0A++++%3Fparagraph+oa%3AhasSource+%3Chttp%3A%2F%2Flinkingdata.io%2Fpmcdoc%2Fpmc%2F3865095%3E+.%0D%0A++++FILTER+NOT+EXISTS+%7B+%3FtermUri+a+oa%3ATextualBody+%7D%0D%0A%7D%0D%0A&should-sponge=&format=text%2Fhtml&timeout=300000&debug=on" target="_blank">Execute it in the endpoint</a>
```

PREFIX oa: <http://www.w3.org/ns/oa#>
PREFIX biotea: <https://biotea.github.io/biotea-ontololgy#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?termUri ?termFrequency ?label
{
    ?annotation a oa:Annotation .
    ?annotation oa:hasTarget ?paragraph .
    ?annotation oa:hasBody ?termUri .
    ?annotation oa:hasBody ?text .
    ?text rdf:value ?label .
    ?annotation biotea:tf ?termFrequency .
    ?paragraph oa:hasSource <http://linkingdata.io/pmcdoc/pmc/3865095> .
    FILTER NOT EXISTS { ?termUri a oa:TextualBody }
}
```

## 6. Biotea + Uniprot + DBPedia
<a href="http://biotea.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+xsd%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0D%0APREFIX+oa%3A%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E%0D%0APREFIX+biotea%3A%3Chttps%3A%2F%2Fbiotea.github.io%2Fbiotea-ontololgy%23%3E+++%0D%0APREFIX+uniprotkb%3A%3Chttp%3A%2F%2Fpurl.uniprot.org%2Fcore%2F%3E++++%0D%0APREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+dbo%3A+%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0A%0D%0ASELECT+DISTINCT+%3FarticleTitle+%3FpmcLink+%3FdbpediaDesc+%28GROUP_CONCAT%28%3FuniprotEntry%3Bseparator%3D%22%7C%22%29+as+%3FuniprotEntries%29%0D%0A++++++WHERE+%7B%0D%0A++++++++%3Fannot+a+oa%3AAnnotation+%3B%0D%0A++++++++++oa%3AhasTarget+%3Fparagraph+%3B%0D%0A++++++++++oa%3AhasBody+%3Chttp%3A%2F%2Fpurl.bioontology.org%2Fontology%2FSNOMEDCT%2F40095003%3E+.%0D%0A++++++++%3Fparagraph+oa%3AhasSource+%3Farticle+.%0D%0A++++++++%3Fannot1+a+oa%3AAnnotation+%3B%0D%0A++++++++++oa%3AhasTarget+%3Fparagraph1+%3B%0D%0A++++++++++oa%3AhasBody+%3Chttp%3A%2F%2Fpurl.bioontology.org%2Fontology%2FSNOMEDCT%2F63730009%3E+.%0D%0A++++++++%3Fparagraph1+oa%3AhasSource+%3Farticle+.%0D%0A++++++++%3Farticle+rdfs%3AseeAlso+%3FpmcLink+.%0D%0A++++++++%3Farticle+dcterms%3Atitle+%3FarticleTitle+.%0D%0A+++++++FILTER%28STRSTARTS%28str%28%3FpmcLink%29%2C+%22http%3A%2F%2Fwww.ncbi.nlm.nih.gov%2Fpmc%2F%22%29%29%0D%0A+++++++%0D%0A++SERVICE+%3Chttps%3A%2F%2Fdbpedia.org%2Fsparql%3E%0D%0A++%7B%0D%0A++++%3Fcalcitonin+rdfs%3Alabel+%3Flabel+.%0D%0A++++%3Fcalcitonin+rdfs%3Acomment+%3FdbpediaDesc+.%0D%0A++++FILTER%28lang%28%3FdbpediaDesc%29+%3D+%27en%27%29%0D%0A++++FILTER%28%3Flabel+%3D+%22Calcitonin%22%40en%29%0D%0A++%7D%0D%0A%0D%0A+++++++SERVICE+%3Chttp%3A%2F%2Fsparql.uniprot.org%2Fsparql%3E+%7B%0D%0A%09%09+%3FuniprotEntry+%3Chttp%3A%2F%2Fpurl.uniprot.org%2Fcore%2FclassifiedWith%3E+%3Chttp%3A%2F%2Fpurl.obolibrary.org%2Fobo%2FGO_0032841%3E+.%0D%0A+++++++%7D%0D%0A%0D%0A%7D+GROUP+BY+%3FarticleTitle+%3FpmcLink+%3FdbpediaDesc&should-sponge=grab-all&format=text%2Fhtml&timeout=300000&debug=on" target="_blank">Execute it in the endpoint</a>
```
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX oa:<http://www.w3.org/ns/oa#>
PREFIX biotea:<https://biotea.github.io/biotea-ontololgy#>   
PREFIX uniprotkb:<http://purl.uniprot.org/core/>    
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX dbo: <http://dbpedia.org/ontology/>

SELECT DISTINCT ?articleTitle ?pmcLink ?dbpediaDesc (GROUP_CONCAT(?uniprotEntry;separator="|") as ?uniprotEntries)
      WHERE {
        ?annot a oa:Annotation ;
          oa:hasTarget ?paragraph ;
          oa:hasBody <http://purl.bioontology.org/ontology/SNOMEDCT/40095003> .
        ?paragraph oa:hasSource ?article .
        ?annot1 a oa:Annotation ;
          oa:hasTarget ?paragraph1 ;
          oa:hasBody <http://purl.bioontology.org/ontology/SNOMEDCT/63730009> .
        ?paragraph1 oa:hasSource ?article .
        ?article rdfs:seeAlso ?pmcLink .
        ?article dcterms:title ?articleTitle .
       FILTER(STRSTARTS(str(?pmcLink), "http://www.ncbi.nlm.nih.gov/pmc/"))
       
  SERVICE <https://dbpedia.org/sparql>
  {
    ?calcitonin rdfs:label ?label .
    ?calcitonin rdfs:comment ?dbpediaDesc .
    FILTER(lang(?dbpediaDesc) = 'en')
    FILTER(?label = "Calcitonin"@en)
  }

       SERVICE <http://sparql.uniprot.org/sparql> {
		 ?uniprotEntry <http://purl.uniprot.org/core/classifiedWith> <http://purl.obolibrary.org/obo/GO_0032841> .
       }

} GROUP BY ?articleTitle ?pmcLink ?dbpediaDesc
```

## 7. Biotea + Open Citations
<a href="http://biotea.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+xsd%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0D%0APREFIX+oa%3A%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Foa%23%3E%0D%0APREFIX+biotea%3A%3Chttps%3A%2F%2Fbiotea.github.io%2Fbiotea-ontololgy%23%3E%0D%0APREFIX+bibo%3A+%3Chttp%3A%2F%2Fpurl.org%2Fontology%2Fbibo%2F%3E%0D%0APREFIX+cito%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Fcito%2F%3E%0D%0APREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0APREFIX+datacite%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Fdatacite%2F%3E%0D%0APREFIX+literal%3A+%3Chttp%3A%2F%2Fwww.essepuntato.it%2F2010%2F06%2Fliteralreification%2F%3E%0D%0APREFIX+biro%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Fbiro%2F%3E%0D%0APREFIX+frbr%3A+%3Chttp%3A%2F%2Fpurl.org%2Fvocab%2Ffrbr%2Fcore%23%3E%0D%0APREFIX+c4o%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Fc4o%2F%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Ftitle+%3FcitedBy+%3Fcited_ref%0D%0AWHERE+%7B%0D%0A++++++++%3Fannot+a+oa%3AAnnotation+%3B%0D%0A++++++++++oa%3AhasTarget+%3Fparagraph+%3B%0D%0A++++++++++oa%3AhasBody+%3Chttp%3A%2F%2Fpurl.bioontology.org%2Fontology%2FSNOMEDCT%2F41607009%3E+.%0D%0A++++++++%3Fparagraph+oa%3AhasSource+%3Farticle+.%0D%0A++++++++%3Farticle+bibo%3Apmid+%3Fpmid+.%0D%0A++++++SERVICE+%3Chttp%3A%2F%2Fopencitations.net%2Fsparql%3E+%7B%0D%0A++++++++++++++%3Fcited+datacite%3AhasIdentifier+%5B%0D%0A%09%09%09datacite%3AusesIdentifierScheme+datacite%3Apmid+%3B%0D%0A%09%09%09literal%3AhasLiteralValue+%3Fpmid%0D%0A%09%09%5D+.%0D%0A+++++++++%3FcitedBy+cito%3Acites+%3Fcited+.%0D%0A%09OPTIONAL+%7B+%0D%0A%09%09%3FcitedBy+frbr%3Apart+%3Fref+.%0D%0A%09%09%3Fref+biro%3Areferences+%3Fcited+%3B%0D%0A%09%09%09c4o%3AhasContent+%3Fcited_ref+%0D%0A%09%7D%0D%0A%09OPTIONAL+%7B+%3Fcited+dcterms%3Atitle+%3Ftitle+%7D%0D%0A++++++%7D%0D%0A%7D&should-sponge=grab-all&format=text%2Fhtml&timeout=0&debug=on" target="_blank">Execute it in the endpoint</a>
```
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX oa:<http://www.w3.org/ns/oa#>
PREFIX biotea:<https://biotea.github.io/biotea-ontololgy#>
PREFIX bibo: <http://purl.org/ontology/bibo/>
PREFIX cito: <http://purl.org/spar/cito/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX datacite: <http://purl.org/spar/datacite/>
PREFIX literal: <http://www.essepuntato.it/2010/06/literalreification/>
PREFIX biro: <http://purl.org/spar/biro/>
PREFIX frbr: <http://purl.org/vocab/frbr/core#>
PREFIX c4o: <http://purl.org/spar/c4o/>

SELECT DISTINCT ?title ?citedBy ?cited_ref
{
  ?annot a oa:Annotation ;
    oa:hasTarget ?paragraph ;
    oa:hasBody <http://purl.bioontology.org/ontology/SNOMEDCT/41607009> .
  ?paragraph oa:hasSource ?article .
  ?article bibo:pmid ?pmid .
  SERVICE <http://opencitations.net/sparql> {
    ?cited datacite:hasIdentifier [
        datacite:usesIdentifierScheme datacite:pmid ;
        literal:hasLiteralValue ?pmid 
      ] .
    ?citedBy cito:cites ?cited .
    OPTIONAL { 
      ?citedBy frbr:part ?ref .
      ?ref biro:references ?cited ;
        c4o:hasContent ?cited_ref
    }
	
    OPTIONAL { ?cited dcterms:title ?title }
  }
}
```
