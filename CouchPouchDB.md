Couch Notes
You need to change you cmder terminal to bash otherwise you will get invalid json when trying to do CURL commands


Add regular user

    curl -X PUT http://localhost:5984/_users/org.couchdb.user:test -d '{"name":"test", "password":"bobspassword", "roles":[], "type":"user"}' -H "Content-Type: application/json"

Add admin user

    curl -X PUT  http://couchadmin:test@localhost:5984/_config/admins/anna -d '"secret"'

    curl -X PUT  http://adminusername:password@localhost:5984/_config/admins/anna -d '"secret"'

View users in fauxton  http://127.0.0.1:5984/_utils/#
Got databases > _users > each item is a user
Change the meta data fields to type, username and roles


When you create a user you can specify any role, essentially this jut is a way to link a user to permissions.  Unlike creating traditional roles then adding them to the users you have to remember the role name you are using so that each user you add has the same role roles name.

In the permissions tab of a database you then specify what roles you want to have admin or member permissions, again you must remember the role names.  It would be nice if they had a drop down list of roles you have created(remember you actually create the role when you add a user), but there is not a nice gui listing the roles you have created.

Get user

    curl GET http://couchadmin:test@localhost:5984/_users/org.couchdb.user:bob