LdapBundle
==========

LDAP bundle for Symfony2

### Configuring directory access

In the most basic case imaginable, a directory server residing on the same
machine as your Symfony2 project, you won't need to configure anything.

Usually, however, the directory server(s) will live somewhere else. Sometimes
you may also want to specify a fallback server, and/or use more than just one
directory. In those cases you need to put a bit of configuration into your
project's config.yml.

This example configuration specifies one directory with master and fallback
servers. If you name your directory `default`, like in this example, you can
omit the `default_directory` option (because `default` is its default value).

```
cisco_ldap:
    default_directory: default
    directories:
        default:
            servers:
                primary:
                    host: ldap.example.com
                secondary:
                    host: ldap2.example.com
```

### Basic usage

```
// Get service
$ldap = $container->get( 'cisco.ldap' );

// Connect to default directory and perform an anonymous bind
$ldap->connect()->bind();

// Connect to specific directory and perform an authenticating bind
$ldap->connect( 'myDir' )->bind( $relativeDistinguishedName, $password );

// Search
$ldap->search( $baseDn, $filter );
```
