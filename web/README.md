# Jon's example web application 

This example web application is written in Go (GoLang).  It will be used as a starting point for any secure web applications that I build. 

### Take it for a spin:
* Run `go build`
* Run `./web`
* Open browser to `http://localhost:8080/secure`
  * notice how it redirects you to https (you will have to set an exception to accept the certificate)
  * when it asks for credentials enter joe@example.com and supersecret

### It currently does these things:
* Redirects to https if http is used
* When started, it builds/rebuilds a sqlite3 user table with example users and passwords
* Provides a couple of resources (/info and /secure)
  * go to http://localhost:8080/secure
  * username: joe@example.com password: supersecret
* HTTP handlers can be wrapped with Basic authentication checks

### It will eventually do these things
* Provide REST resources that:
  * return user data as JSON (from the user table)
  * inserts and updates data in the user table
* Web pages to display users, edit them, and create new ones
* Prevent brute force password attack by blocking account for 20 minutes after 10 invalid passwords are tried

### Libraries used:
* net/http          
* https://github.com/jmoiron/sqlx - maps rows to objects
* https://github.com/mattes/migrate - handles database migration
* https://github.com/stvp/assert - assertions for testing
* Bootstrap for styling web pages
* Angular JS for browser->server interactions

### I may use these libraries:
* gorilla/mux:        go get -u github.com/gorilla/mux
* codegansta/negroni: go get -u github.com/codegangsta/negroni

### How to recreate the DB using the command-line
migrate -url sqlite3://web.db -path ./migrations reset
migrate -url sqlite3://web.db -path ./migrations up

### Future ideas for startup
* `./web --url 'sqlite3://database.db' --https-cert=https-cert.pem --https-key=https-key.pem`
* create a web.sh script to start it up with the above command