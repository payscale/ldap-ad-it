# Simple LDAP server simulating AD for integration testing

This is a simple LDAP server that tries to simulate an AD using 
Apache Directory Server.

* It has had basic testing with:
   * [ActiveDirectory for Node](https://www.npmjs.com/package/activedirectory)
   * [LDAP for PHP](http://php.net/manual/en/book.ldap.php)
* Is based on 
   * https://github.com/kwart/ldap-server/ and 
   * http://stackoverflow.com/questions/11174835/add-memberof-attribute-to-apacheds
   * And, forked from https://github.com/dwimberger/ldap-ad-it

## Running

To just get _something_ running with some test data:

```bash
docker run -it --rm -p 389:10389 psdocker/ldap-ad-it
```

### Customized Values

You'll likely want to run some customized users/OUs/etc. To do that, you can
mount a file into `/ldap/users.ldif`. An example:

```bash
docker run -d --name=ldap-ad-it --rm \
        -v $PWD/testdata/users.ldif:/ldap/users.ldif \
        -p 389:10389 \
        psdocker/ldap-ad-it:latest
```

I do not recommend writing your own LDIF file by hand. I used an OpenLDAP
server and phpldapadmin to configure what I wanted, then exported and tuned
from there. [I used this toolset](https://github.com/osixia/docker-phpLDAPadmin#openldap--phpldapadmin-in-1).

## Building

1. Build image `docker build -t psdocker/ldap-ad-it .`
2. Run the image using  
   `docker run -it --rm -p 389:10389 psdocker/ldap-ad-it`
