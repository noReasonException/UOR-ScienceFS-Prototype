# This is the ElasticSearch version of ScienceFS prototype

*If you want to play directly with it without reading all the boring notes skip the first page*

*The main file is parser.py*

It takes 4 parameters

### (-u) the url link of any elasticSearch node , for example if you host locally ...
```
	http://localhost:9200/
```
Note! do not specify index or type yet! just the URI
### (-q) the query

The query to ElasticSearch , it must be of the form...
```	
	<IndexName>|{<ElasticSearch Query>}
```
The call in the background will be the following , the curl equilevant will be
```
	curl -XGET '<your url>/<IndexName>/_search' -d '{<your query>}'
```
### (-m) the mount point
	
*@Note The mount point must already exists*

### (-n) the namespace structure

#### How you want to structure the files?
for example , you may want to structure it as 
```
	/variableName/modelName/experimentName 
```
and every file inside to have the experiment period , then the following -n parameter must passed
```
	-n variable/model/experiment.name:experiment.period
```
*@Note , the ':' splits the namespace structure from the contents of the file , only one field can exist inside the file 
*@TODO : this feature will removed in the next version!


# Lets play with it (Local computer)

1) run the configure script , passing the url of any ElasticSearch node as first  parameter
```
	./configure.sh http://localhost:9200
```

This will install the nessesary modules (fusepy,elasticsearch and others...) and will insert 3 plain samples on your db

2) run ...
```
sudo python parser.py -u http://localhost:9200 -q 'experiments16001700|{"query":{"match_all":{}}}' -n variable/model/experiment.name:experiment.period -m tst/mnt2
```
3) play ...

	1. try different queries on -q parameter 
	2. play with namespace structure parameter (-n)
	3. always kill with -9 before re-run , otherwise you may need restart to restore the proper state on the test folder (its a prototype <3 ) 
	4. enjoy!


## Lets play with it (in the cluster) 

same as above , but you will need to run ./configureBIG 
*@TODO : well.. basically write the ./configureBIG *
*@NotApplicableYet*
	

	
