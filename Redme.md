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


data: '{{hub copySecretData "policies" "my-secret" hub}}'


"ns-936.awsdns-53.net",
"ns-1853.awsdns-39.co.uk",
"ns-1497.awsdns-59.org",
"ns-481.awsdns-60.com"


LE_POLICY_ARN=$(aws iam list-policies --output json --query 'Policies[*].[PolicyName,Arn]' --output text | grep letsencrypt-wildcard | awk '{print $2}')
aws iam create-group --group-name letsencrypt-wildcard
aws iam attach-group-policy --policy-arn ${LE_POLICY_ARN} --group-name letsencrypt-wildcard
aws iam create-user --user-name letsencrypt-wildcard
aws iam add-user-to-group --user-name letsencrypt-wildcard --group-name letsencrypt-wildcard
aws iam create-access-key --user-name letsencrypt-wildcard



extradependency - https://redhat-internal.slack.com/archives/CU4QXLPQB/p1694016791286889

LE_POLICY_ARN=$(aws iam list-policies --output json --query 'Policies[*].[PolicyName,Arn]' --output text | grep letsencrypt-wildcard | awk '{print $2}')
aws iam create-policy --policy-name letsencrypt-wildcard --policy-document file://letsencrypt-wildcard.json
aws iam create-group --group-name letsencrypt-wildcard
aws iam attach-group-policy --policy-arn ${LE_POLICY_ARN} --group-name letsencrypt-wildcard
aws iam create-user --user-name letsencrypt-wildcard
aws iam add-user-to-group --user-name letsencrypt-wildcard --group-name letsencrypt-wildcard
aws iam create-access-key --user-name letsencrypt-wildcard
 oc create secret generic aws-route53-creds --from-literak=awsSecretAccessKey="XeUxHyOXpLdsEF9/+Sq6IdrofQAwT+f3PwKQdAiA" -n cert-manager\n

 ArgoCD:
 oc adm policy add-cluster-role-to-user cluster-admin -z openshift-gitops-argocd-application-controller -n openshift-gitops
