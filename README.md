# IBPv2 Enablement Session

## Pre-requisites

To follow along with this tutorial, you will first need to follow these steps:

1. Ensure that you have all of the pre-requisites installed: https://github.com/IBM-Blockchain/ansible-role-blockchain-platform-manager#requirements

2. Install all required roles, including the `ibm.blockchain_platform_manager` role, from Ansible Galaxy:

   `ansible-galaxy install -r requirements.yml --force`

## Set up the network

In this tutorial, we're going to use an Ansible playbook to build a Hyperledger Fabric network with two organizations, `Org1` and `Org2`. Each organization has two peers. The two peers are configured with a single channel, `channel1`. The FabCar sample contract is instantiated on this channel, with an endorsement policy stating that both organizations must endorse any transactions.

### Create an instance of the IBM Blockchain Platform

Coming soon!

### Spin up the network

This Ansible playbook defaults to deploying to Docker. To configure the Ansible playbook to deploy to the IBM Blockchain Platform on IBM Cloud, follow these steps:

1. Edit the playbook such that the `infrastructure.type` variable is set to `saas`:

```yaml
infrastructure:

type: saas

saas: "{{ lookup('file', 'service-creds.json') | from_json }}"
```

2. Create a file named `service-creds.json` that contains valid service credentials from your IBM Blockchain Platform service instance on IBM Cloud. These service credentials should be of the format:

```json
{
  "api_endpoint": "https://xxxxxx-optools.uss02.blockchain.cloud.ibm.com",

  "apikey": "xxxxxx",

  "configtxlator": "https://xxxxxx-configtxlator.uss02.blockchain.cloud.ibm.com",

  "iam_apikey_description": "Auto-generated for key xxxxxx",

  "iam_apikey_name": "xxxxxx",

  "iam_role_crn": "crn:v1:bluemix:public:iam::::serviceRole:Manager",

  "iam_serviceid_crn": "crn:v1:bluemix:public:iam-identity::a/xxxxxx::serviceid:ServiceId-xxxxxx"
}
```

3. Run the Ansible playbook:

   `ansible-playbook playbook.yml`

4. Head over to your instance of the IBM Blockchain Platform running on IBM Cloud. You should now see your Peers, Certificate Authorities and Orderer running, like the below:

<img src="./images/Console.png" />

Information on the available nodes (peers, orderers, and certificate authorities) will be created under the `nodes` subdirectory. Since you are using the IBM Blockchain Platform on IBM Cloud, you **do not** need to import these JSON files. All of the nodes will already be present in your web console.

## Import the identities

The `wallets` subdirectory will contain all of the identities (certificates and private keys) enrolled by this playbook. You must be careful to persist all of these files for the next time you run this playbook, otherwise you will be unable to administer your IBM Blockchain Platform network.

Since you are using the IBM Blockchain Platform on IBM Cloud, you **do** need to import these JSON files into your wallet using the web console. You will then need to assiociate each node with the correct identity. If you do not do this, then you will be unable to administer the nodes using the web console.

## Submit a transaction

Coming soon!

## Upgrade the smart contract
