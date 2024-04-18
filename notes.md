# Notes

Source: <https://github.com/aborroy/alfresco-identity-service-to-keycloak?tab=readme-ov-file>

- [How can I allow Authorization - Bearer token in alfresco rest requests?](https://hub.alfresco.com/t5/alfresco-content-services-forum/how-can-i-allow-authorization-bearer-token-in-alfresco-rest/td-p/179011)
  > Hello,

  Instead Bearer you should use the alf_ticket param in your curl call. First thing you do is call the login web script to get a ticket.

  ```bash
  curl -v "http://localhost:8080/alfresco/service/api/login?u=admin&pw=yourpassword"
  ```

  Alfresco will respond with something like:

  ```bash
  TICKET_e46107058fdd2760441b44481a22e7498e7ddfsf
  ```

  Now you can take that ticket and append it to your subsequent web script calls.

  Then post it to the web script using curl, like this:

  ```bash
  curl -v -X POST "http://localhost:8080/alfresco/service/someco/someScript?alf_ticket=TICKET_e46107058fdd2760441b44481a22e7498e7dbf66" -H "Content-Type: application/json" -d @/Users/arjunm/test.json
  ```

- https://github.com/Acosix/alfresco-keycloak/issues/15
  > _If **I don't configure the connector** in Alfresco Connector in the Share tier (share-config-custom.xml without <id>alfrescoCookie</id> and the remaining entries to redirect endpoints to /wcs ), **I am able to authenticate to Repo and Share** tiers using Keycloak users._

- [Login To Alfresco API](https://hub.alfresco.com/t5/alfresco-content-services-forum/login-to-alfresco-api/td-p/205455)
  > _If you have obtained a ticket from /alfresco you can use other ReST APIs on /alfresco to interact with the content of the system using the ticket as your authentication token. You can also use the ticket via CMIS using the special user name "ROLE_TICKET" and the ticket as the password._

- OpenLDAP Support: <https://hub.alfresco.com/t5/alfresco-content-services-forum/alfresco-6-2-showing-the-basic-auth-dialog-when-accessing-to/td-p/304303>

- Sample:

  ```bash
  curl -v "http://localhost:8080/alfresco/service/api/login?u=admin&pw=admin"

  curl -v "http://localhost:8080/alfresco/service/api/login?u=test&pw=admin"

  ###############

  curl -X GET "http://localhost:8080/alfresco/api/-default-/public/alfresco/versions/1/action-definitions?skipCount=0&maxItems=100&alf_ticket=TICKET_56f1dc3fa3b24218c9780e73e116ab19ad3c02b5" -H "Content-Type: application/json"
  ```
