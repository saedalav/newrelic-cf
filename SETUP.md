# Deploying NewRelic Service to Monitor Addressapi and Adressapiclient Applications on PCF
*** 

### Setting up the Project: 

##### Prerequisites: 
You need to have a valid New Relic Account. See here: 
https://rpm.newrelic.com

Then, login to your New Relic Account and record the License Key from here:
https://rpm.newrelic.com/accounts


1. Clone this Project 
```sh
git clone https://github.com/saedalav/newrelic-cf.git 
cd newrelic-cf.git
```
2. Edit manifest.yml file and update your Username, password, and New Relic License Key. 
```sh 
vim manifest.yml
[ Update ] 
:wq
```

3. Execute the following commands: 

```sh 
cf login -a URL -u USERNAME -p PASSWORD
cf push 
cf create-service-broker newrelicservicebroker saedalav mypass https://newrelicservicebrokerapp.apps.alavinia.me 
cf enable-service-access newrelic
cf create-service newrelic standard newrelicserviceinstance
cf bind-service addressapi newrelicserviceinstance
cf bind-service addressapiclient newrelicserviceinstance
cf restage addressapi
cf restage addressapiclient
```