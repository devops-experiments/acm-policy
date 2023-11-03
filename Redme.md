Demo Plan: 
SSO Steps:
1. Keycload client id secret for each cluster in hub. OAuth client id secret, issuer url. 
2. Policy propagates the secret to the managed cluster.
3. Policy to create OAuth, the group sync operator and the instance


Cert-Manager Steps:
1. setup lets encrypt
2. install cert-manager through policy

ESO Operator:
1. Install ESO
2. Dopler token