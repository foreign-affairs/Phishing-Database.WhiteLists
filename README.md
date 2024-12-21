# Alpha release note

This whitelist repo is thought to match the following issues and disquisitions

- https://github.com/Phishing-Database/dev-center/issues/10
- https://github.com/Phishing-Database/dev-center/discussions/9

The folder/files are structured to meat the rule handling of [tivilsta]
(https://github.com/funilrys/tivilsta) the significantly enhanced version of
its python related version [whitelist](https://github.com/Ultimate-Hosts-Blacklist/whitelist/tree/script).

## Rule types

- `all.lst` This list are for ALL rules _ONLY_. See mechanism below
- `literal.lst` This is for literal exceptions, the No Flag rule. See
  mechanism below
- `regex.lst` This is for the REG+RZD rules. Even though we could help keeping
  the files smaller by separating these in two and use the `--reg` and
  `--rzd` flags, the in the reality, we would add more load to the repo
  system by doing this, as the number of records are very few. See mechanism
  below
