NOT FINISH -- IN PROGRESS

TODO
----

1. Finir le docker-compose

MapServer :
	- Override l'instance web (nginx) avec la gestion de mapserver
	- Ou si Mapserver sera dans l'instance web ou dans une autre séparé
	- Et ajouter l'extention php_mapscript au container PHP (5.6 puis travailler sur l'évolution en 7 quand la compatibilité mapscript sera ok)

Amélioration (docker-compose.dist.yml) :
	- Augmenter la Stack Optimisation (Ex : Varnish)
	- Augmenter la Stack ElasticSearch (Ex : Kibana, Logstash)
	- Ajouter la vue d'ensemble des containers avec le système proposé par Docker (voir site officiel)

2. Rédiger le README