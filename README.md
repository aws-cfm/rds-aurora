[![Build Status](https://travis-ci.org/aws-cfm/rds-aurora.svg?branch=master)](https://travis-ci.org/aws-cfm/rds-aurora)
[![NPM version](https://img.shields.io/npm/v/@aws-cfm/rds-aurora.svg)](https://www.npmjs.com/package/@aws-cfm/rds-aurora)

# cfn-modules: RDS Aurora

RDS Aurora with secure firewall configuration, encryption, multi AZ, auto scaling, backup enabled, and alerting.

## Install

> Install [Node.js and npm](https://nodejs.org/) first!

```
npm i @cfn-modules/rds-aurora
```

## Usage

```
---
AWSTemplateFormatVersion: '2010-09-09'
Description: 'cfn-modules example'
Resources:
  Cluster:
    Type: 'AWS::CloudFormation::Stack'
    Properties:
      Parameters:
        VpcModule: !GetAtt 'Vpc.Outputs.StackName' # required
        ClientSgModule: !GetAtt 'ClientSg.Outputs.StackName' # required
        AlertingModule: '' # optional
        BastionModule: '' # optional
        HostedZoneModule: '' # optional
        KmsKeyModule: '' # optional
        Engine: 'aurora' # optional
        DBSnapshotIdentifier: '' # optional
        DBInstanceClass: 'db.t2.small' # optional
        DBName: 'mydb' # optional
        DBBackupRetentionPeriod: 30 # optional
        DBMasterUsername: 'master' # optional
        DBMasterUserPassword: 'password' # optional
        SubDomainNameWithDot: 'aurora.' # optional
        ReadSubDomainNameWithDot: 'read-aurora.' # optional
        PreferredBackupWindow: '09:54-10:24' # optional
        PreferredMaintenanceWindow: 'sat:07:00-sat:07:30' # optional
      TemplateURL: './node_modules/@cfn-modules/rds-aurora/module.yml'

```

## Examples

none

## Related modules

none

## Parameters

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Description</th>
      <th>Default</th>
      <th>Required?</th>
      <th>Allowed values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>VpcModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/vpc">vpc module</a></td>
      <td></td>
      <td>yes</td>
      <td></td>
    </tr>
    <tr>
      <td>ClientSgModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/client-sg">client-sg module</a></td>
      <td></td>
      <td>yes</td>
      <td></td>
    </tr>
    <tr>
      <td>AlertingModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/alerting">alerting module</a></td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>BastionModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/search?q=keywords:cfn-modules:Bastion">module implementing Bastion</a></td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>HostedZoneModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/search?q=keywords:cfn-modules:HostedZone">module implementing HostZone</a></td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>KmsKeyModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/kms-key">kms-key module</a></td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>Engine</td>
      <td>Aurora engine and version</td>
      <td>aurora</td>
      <td>no</td>
      <td>['5.6.mysql-aurora.1.19.1', 'aurora', '5.7.mysql-aurora.2.04.3', '5.7.mysql-aurora.2.03.4', 'aurora-mysql', 'aurora-postgresql-10.7', 'aurora-postgresql-10.6', 'aurora-postgresql-10.5', 'aurora-postgresql-10.4', 'aurora-postgresql-9.6.12', 'aurora-postgresql']</td>
    </tr>
    <tr>
      <td>DBSnapshotIdentifier</td>
      <td>The identifier for the DB cluster snapshot from which you want to restore (leave blank to create an empty cluster).</td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>DBInstanceClass</td>
      <td>he instance type of database server.</td>
      <td>db.t2.small</td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>DBName</td>
      <td>Name of the database (ignored when DBSnapshotIdentifier is set, value used from snapshot).</td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>DBBackupRetentionPeriod</td>
      <td>The number of days to keep snapshots of the cluster.</td>
      <td>30</td>
      <td>no</td>
      <td>1-35</td>
    </tr>
    <tr>
      <td>DBMasterUsername</td>
      <td>The master user name for the DB instance (ignored when DBSnapshotIdentifier is set, value used from snapshot).</td>
      <td>master</td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>DBMasterUserPassword</td>
      <td>The master password for the DB instance (ignored when DBSnapshotIdentifier is set, value used from snapshot).</td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>SubDomainNameWithDot</td>
      <td>Name that is used to create the DNS entry with trailing dot, e.g. §{SubDomainNameWithDot}§{HostedZoneName}. Leave blank for naked (or apex and bare) domain. Requires HostedZoneModule parameter!</td>
      <td>aurora.</td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>ReadSubDomainNameWithDot</td>
      <td>Name that is used to create the read DNS entry with trailing dot, e.g. §{SubDomainNameWithDot}§{HostedZoneName}. Leave blank for naked (or apex and bare) domain. Requires HostedZoneModule parameter!</td>
      <td>read-aurora.</td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>PreferredBackupWindow</td>
      <td>The daily time range in UTC during which you want to create automated backups.</td>
      <td>09:54-10:24</td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>PreferredMaintenanceWindow</td>
      <td>The weekly time range in UTC during which system maintenance can occur.</td>
      <td>sat:07:00-sat:07:30</td>
      <td>no</td>
      <td></td>
    </tr>
  </tbody>
</table>

## Outputs

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Description</th>
      <th>Export</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ModuleId</td>
      <td>The ID of module: `ecs-cluster`</td>
      <td></td>
    </tr>
    <tr>
      <td>ModuleVersion</td>
      <td>The version of module: `1.0.0`</td>
      <td></td> 
    </tr>
    <tr>
      <td>StackName</td>
      <td>The name of CloudFormation Stack</td>
      <td></td>
    </tr>
    <tr>
      <td>ClusterName</td>
      <td>The name of the database cluster.</td>
      <td>`${AWS::StackName}-ClusterName`</td> 
    </tr>
    <tr>
      <td>DNSName</td>
      <td>The connection endpoint for the DB cluster.</td>
      <td>`${AWS::StackName}-DNSName`</td> 
    </tr>
    <tr>
      <td>ReadDNSName</td>
      <td>The reader endpoint for the DB cluster.</td>
      <td>`${AWS::StackName}-ReadDNSName`</td> 
    </tr>
  </tbody>
</table>
