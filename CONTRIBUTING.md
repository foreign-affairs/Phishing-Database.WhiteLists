To contribute you have to be an approved team member, see 
README#phishing-database-whitelist, everyone else have to use the issue

## Phishing database Whitelist

Phishing database Whitelist is the repository for handling False positives 
found within any of [Phishing database](https://github.com/Phishing-Database)
subprojects. You as user are only permitted to report potential False 
Positive via the [issue tickets](), as all Merge Requests from none members 
of the following teams: [contributors](https://github.com/orgs/Phishing-Database/teams/contributors),
[safekeepers](https://github.com/orgs/Phishing-Database/teams/safekeepers) and
[maintainers](https://github.com/orgs/Phishing-Database/teams/maintainers)
**WILL** be closed without comment or further handling, just like that. ...No 
remorse nor regrets.

## Writing rules

### File and folder structure

The repository contains 3 folder, that by the names should be rather self 
explaining for their usage. Yet the explainer have the word...

`any/` Rules that should be covering whitelisting of **_both_** domain 
**and** URI types
`domain` Rules that **_only_** should be covering whitelisting of domain types
`uri` Rules that **_only_** should be covering whitelisting of URI types

Within these folders we find equally looking files for writing exception 
rules for the Phishing Database. The files could as well just have been one 
file, thanks to how Tivilsta are operated, but to help keeping the files 
small and easier to oversight, they are divided into:

- `all.lst` This list are for ALL rules _ONLY_. See mechanism below
- `literal.lst` This is for literal exceptions, the No Flag rule. See 
  mechanism below 
- `regex.lst` This is for the REG+RZD rules. Even though we could help keeping 
  the files smaller by separating these in two and use the `--reg` and 
  `--rzd` flags, the in the reality, we would add more load to the repo 
  system by doing this, as the number of records are very few. See mechanism 
  below

Tivilsta provides a set of flags to make whitelist maintenance easier.

### No Flag - The literal rule

This is the purest of all rules. It is what we all know an cherish. The single
line without any flag.

```txt
example.org
```

In this example, any subject of your source file that literally matches `example.org`
will be whitelisted.

### ALL - The ends-with rule

Sometime when working with highly volatile dataset, you may want to whitelist
every subjects that ends with for example `gov.uk`.

With Tivilsta you can do that through the `ALL ` flag.

```regexp
ALL .gov.uk
```

In this example, any subject of your source file that ends with `.gov.uk` -
`gov.uk` included - will be whitelisted.

### REG - The regular expression rule

You are a fan of regex ? We are too! When working with highly volatile dataset,
we want to simply use a regular expression (short regex) to do the task.

With Tivilsta you can do that through the `REG ` flag.

```regexp
REG ^(?!.*\.?(watchdog\.ohio|dap\.digitalgov|stats\.ssa|adgallery\.whitehousedrugpolicy)).*\.gov$
```

In this example, any subject of your source file that ends with `.gov` will be
whitelisted except the following:

- `watchdog.ohio.gov`
- `dap.digitalgov.gov`
- `stats.ssa.gov`
- `adgallery.whiteshousedrugpolicy.gov`

### RZD - The broad and powerful rule

Have you ever wondered if it is possible to somehow whitelist all combination of
a company name with all possible Top Level Domain ?

With Tivilsta you can do that through the `RDZ ` flag. This flag is extremely
broad and powerful as it will fetch the
[IANA Root Zone Database](https://www.iana.org/domains/root/db) and the
[Public Suffix List](https://publicsuffix.org/)
to build a set of rules with all possible gTLDs or extensions - if you prefer.

```
RZD example
```

In this example, any subject matching `example.[gTLD]` will be whitelisted.

### Note

See full man page here https://github.com/funilrys/tivilsta?tab=readme-ov-file#the-flags
