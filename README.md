# Rijksmuseum Newman API Test

Testframework in Postman/Newman to test the [Rijksmuseum Data Services](https://data.rijksmuseum.nl/docs/).

## How to run the tests ##

### Environment Variables ###

| key      | value                            |
|----------|----------------------------------|
| baseurl  | "https://www.rijksmuseum.nl/api" |
| key      |                                  |


### Local ### 

#### Postman ####

To run the test locally import into postman:
 - collections/regression_testing.postman_collection.json 
 - environments/rijks.postman_environment.json

Make sure your apikey is filled in and run a specified test from the scenario based folder. If you want to run the data_driven tests, please use a runner tab and upload the json testdata document. 

#### Newman #### 

To run the test locally with newman install node.js and use the following command:
	  npx newman run collections/regression_testing.postman_collection.json \
	    -e environments/rijks.postman_environment.json \
	    -r cli \
	    --folder "scenario_based"

### CI/CD ###

To run the pipeline checkout 'main' branch and do an empty commit.

git commit --allow-empty -m "Trigger pipeline"
git push

To see the report, navigate to [Github Pages](https://alebr001.github.io/rijksmuseum_api_assessment_pm/)


## Findings ##

* When using Collection Details without an object-number there is no error message, or functional feedback
* Malformed format leads to 404
* Empty format leads to http500 
* Internal server error does nog have a good error handling (no output)
* When format is jsonp is generates a contenttype of text/javascript while application/javascript is considered best practice. 