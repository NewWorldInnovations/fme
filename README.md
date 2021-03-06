# fme
FundMeDaddy


###### Setup virtual environments
    virtualenv -p python3 envFMEmaster
    cd envFMEmaster
    source bin/activate
    git clone https://github.com/NewWorldInnovations/fme.git
    cd fme
    pip install -r requirements.txt
    python manage.py runserver
    
###### Restful API links
   * ```/api/```                          <=== namespace for api but doesn't have view/get
   * ```/api/token/auth/```               <=== to obtain user login token
   * ```/api/token/refresh/```            <=== logic wise its a token refresh :)
   * ```/api/token/verify/```             <=== Verify as usual
   * ```/api/login/```                    <=== login (post)
   * ```/api/register/```                 <=== register (Create)
   * ```/api/members/```                  <=== members (Retrieve) admin only
   * ```/api/events/```                   <=== Create (List if Get/Create if POST)
   * ```/api/events/<event_id>```         <=== RUD (Retrieve/Update/Delete) methods: (-X GET) (-X PUT) (-X DELETE)
   * ```/api/wishlist/```                 <=== event_id pass to wish create view for object foreign key purposes OR can be direct as long as included in post eg: {"eid":"<event_id>"}
   * ```/api/wishlist/<event_id>```       <=== RUD (Retrieve/Update/Delete) methods: (-X GET) (-X PUT) (-X DELETE)

###### View API
  1. Normal link will show you BrowsableAPI
  2. adding ```?format=json``` will give you a json raw result
   
###### Obtain Token
    curl -X POST -H "Content-Type: application/json" -d '{"username":"**testuser6**","password":"**testuser69**"}' http://localhost:8000/api/token/auth/ 
    
  * Response
    ```{"token":"<generated_token>"}```
    
###### Refresh Token
    curl -X POST -H "Content-Type: application/json" -d '{"token":"<EXISTING_TOKEN>"}' http://localhost:8000/api/token/refresh/
    
###### Verify Token after refresh
    curl -X POST -H "Content-Type: application/json" -d '{"token":"<EXISTING_TOKEN>"}' http://localhost:8000/api/token/verify/

  
###### Sample GET
    curl -H "Authorization: JWT <token>" http://localhost:8000/api/events/*
        
###### Sample POST Event to current user (kindly check edate format)
    curl -X POST -H "Authorization: JWT <token>" -H "Content-Type: application/json" -d '{"title":"Test Event 2","desc":"This is a test for curl","edate":"2018-07-23T02:22:43Z","target_fund":"3500","status":"inc","visibleto":"all"}'  http://localhost:8000/api/events/
        
        
    
