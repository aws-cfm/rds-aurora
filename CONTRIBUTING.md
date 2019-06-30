# Contributor Guide

## Update RDS Auora engine version

```
$ aws rds describe-db-engine-versions --engine aurora --query 'DBEngineVersions[?contains(SupportedEngineModes,`provisioned`)].EngineVersion'
$ aws rds describe-db-engine-versions --engine aurora-mysql --query 'DBEngineVersions[?contains(SupportedEngineModes,`provisioned`)].EngineVersion'
$ aws rds describe-db-engine-versions --engine aurora-postgresql --query 'DBEngineVersions[?contains(SupportedEngineModes,`provisioned`)].EngineVersion'
```
