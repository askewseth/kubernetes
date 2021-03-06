# Running the Appication:
    - The application is able to be run either as a local docker container or as a kubernetes pod
    - If you want to run the application as a kubernetes pod, you can use the included bash script 'k8.sh' to run the application, the steps are as follows:
        - ./k8.sh create //creates the pod locally
        - ./k8.sh expose //exposes the pods 5555 port to your hosts 5555 port so you can access the API
    - The api runs on port 5555, so if you're running the application locally and want to get the list of all of the books you can enter: http://localhost:5555/books in your browser 
    

# API Definitions:
     Model Definitions:
        Book:
            {
                "id": [uuid v4],
                "title": [string],
                "author": [string],
                "publisher": [string],
                "publish_date": [string format:2018-01-02T15:04:05Z],
                "rating": [int:1-3],
                "status": [
                            taken in as int: 0|1,
                            returned as string: CheckedIn|CheckedOut
                          ]
            }

    Endpoint Definitions:
        GET /books
            - Returns a list of all of the books that have been created

        GET /books/{id}
            - Returns a single book given it's id
            - Will return a 404 if the given id isn't found

        POST /books
            - Creates a new book, any subset of the above fields can be given in the POST body to create a new book
            - The id field, if given, will be overwritten. 
            - Will return a 400 if any of the fields given are invalid

        PUT /books/{id}
            - Will update a book when given any subset of the above model fields in the PUT body. 
            - Will return a 404 if the given id isn't found
            - Will return a 400 if any of the fields given are invalid

        DELETE /books/{id}
            - Will remove a book from the API's memory
            - Will return a 404 if the id isn't found
