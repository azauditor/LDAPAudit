# LDAPAudit

This command-line is run to provide a listing of all users that are in the ldap file.

## Switch

-s "scope"

    Specify the scope of a search.  The *scope* parameter may have one of the following values:
        - base - For searching only the base entry
        - one - For searching only the children of the base entry.
        - sub - For searching the base entry and all its descendants.

-p "port" (deprecated see -H)

    Specifies the TCP port number that the Directory Server uses. For example, -p 1049. The default is 389. If -Z is used, the default is 636.

-W "password"

    Prompt for simple authentication. This is used instead of specifying the password on the command line.

-D "bindDN"

    Specifies the distinguished name with which to authenticate to the server. This is optional if anonymous access is supported by the server. If specified, this value must be a DN recognized by the Directory Server, and it must also have the authority to search for the entries. For example, -D "uid=bjensen, dc=example,dc=com".

-h "hostname" (deprecated see -H)

    Specifies the hostname or IP address of the machine on which the Directory Server is installed. For example, -h mozilla. If a host is not specified, ldapsearch uses the localhost.

-b "baseDN"

    Specifies the starting point for the search. The value specified here must be a distinguished name that currently exists in the database. This is optional if the LDAP_BASEDN environment variable has been set to a base DN. The value specified in this option should be provided in single or double quotation marks. For example:
        -b "cn=Barbara Jensen, ou=Product Development,dc=example,dc=com"
    To search the root DSE entry, specify an empty string here, such as -b "".

-H "Hostname"

    Specify URI(s) referring to the ldap server(s); a list of URI, separated by whitespace or commas is expected; only the protocol/host/port fields are allowed. As an exception, if no host/port is specified, but a DN is, the DN is used to look up the corresponding host(s) using the DNS SRV records, according to RFC 2782. The DN must be a non-empty sequence of AVAs whose attribute type is "dc" (domain component), and must be escaped according to RFC 2396.

-L "Display Results"

    Search results are display in LDAP Data Interchange Format detailed in ldif(5). A single -L restricts the output to LDIFv1. A second -L disables comments. A third -L disables printing of the LDIF version. The default is to use an extended version of LDIF.

-o "opt"

    Specify general options.

    ldif-wrap=no - Allows the exported data to not wrap to a new line if the line information is over 78 characters.

For the full list of switches refer to the ldapsearch man page or consult your organization preferred Linux manual web page.

## Command Line Code

The following command line is using the current iteration of the ldapsearch protocol.

``` shell
ldapsearch -LLL -o ldif-wrap=no -s sub "(objectclass=*)" -W -D "uid=bjensen, dc=example,dc=com" -H hostname -b "dc=example,dc=com"  > ldapresults.ldif
```

The following command line is using deprecated switches "-h, -p" however it is still provided in case the environment does not support the newer switch "-H".

``` shell
ldapsearch -LLL -o ldif-wrap=no -s sub "(objectclass=*)" -p 389 -W -D "uid=bjensen, dc=example,dc=com" -h hostname -b "dc=example,dc=com"  > ldapresults.ldif
```