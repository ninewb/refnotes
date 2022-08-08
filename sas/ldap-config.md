# LDAP Configuration

A base dn is the point from where a server will search for users. So I would try to simply use `admin` as a login name.

Most ldap aware applications, this is what is going to happen:


1. An ldap search for the user `admin` will be done by the server starting at the base dn (`dc=example,dc=com`).
2. When the user is found, the full dn (`cn=admin,dc=example,dc=com`) will be used to bind with the supplied password.
3. The ldap server will hash the password and compare with the stored hash value. If it matches, you're in.

Getting step 1 right is the hardest part, but mostly because we don't get to do it often. Things you have to look out for in your configuraiton file are :


- The `dn` your application will use to bind to the ldap server. This happens at application startup, before any user comes to authenticate. You will have to supply a full dn, maybe something like `cn=admin,dc=example,dc=com`.
- The authentication method. It is usually a "simple bind".
- The user search filter. Look at the attribute named `objectClass` for your `admin` user. It will be either `inetOrgPerson` or `user`. There will be others like `top`, you can ignore them. In your openca configuration, there should be a string like `(objectClass=inetOrgPerson)`. Whatever it is, make sure it matches your admin user's object Class. You can specify two object class with this search filter `(|(objectClass=inetOrgPerson)(objectClass=user))`.

Download an LDAP Browser, such as [Apache's Directory Studio](http://directory.apache.org/studio/). Connect using your application's credentials, so you will see what your application sees.
