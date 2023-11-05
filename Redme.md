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


{
    "User": {
        "Path": "/",
        "UserName": "letsencrypt-wildcard",
        "UserId": "AIDAXP7MSJU22BJAFVMQA",
        "Arn": "arn:aws:iam::515355331893:user/letsencrypt-wildcard",
        "CreateDate": "2023-11-04T01:01:24+00:00"
    }
}


{
    "AccessKey": {
        "UserName": "letsencrypt-wildcard",
        "AccessKeyId": "AKIAXP7MSJU2YL3NGJMO",
        "Status": "Active",
        "SecretAccessKey": "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",
        "CreateDate": "2023-11-04T01:01:46+00:00"
    }
}

AWS_ACCESS_KEY_ID=AKIAXP7MSJU2YL3NGJMO
AWS_SECRET_ACCESS_KEY=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
echo ${AWS_SECRET_ACCESS_KEY} > password.txt
kubectl create secret generic aws-route53-creds --from-file=password.txt -n cert-manager
rm -f password.txt


extradependency - https://redhat-internal.slack.com/archives/CU4QXLPQB/p1694016791286889

{
    "Location": "https://route53.amazonaws.com/2013-04-01/hostedzone/Z06980682AOK39QIUB1QQ",
    "HostedZone": {
        "Id": "/hostedzone/Z06980682AOK39QIUB1QQ",
        "Name": "aychandr.shop.",
        "CallerReference": "2023-11-04:18:45",
        "Config": {
            "PrivateZone": false
        },
        "ResourceRecordSetCount": 2
    },
    "ChangeInfo": {
        "Id": "/change/C08792133IUVK44KK2ZCD",
        "Status": "PENDING",
        "SubmittedAt": "2023-11-04T22:45:10.762000+00:00"
    },
    "DelegationSet": {
        "NameServers": [
            "ns-567.awsdns-06.net",
            "ns-265.awsdns-33.com",
            "ns-1801.awsdns-33.co.uk",
            "ns-1522.awsdns-62.org"
        ]
    }
}


Unable to create application: application spec for policies is invalid: InvalidSpecError: Unable to generate manifests in ./: rpc error: code = Unknown desc = Manifest generation error (cached): `kustomize build <path to cached source> --enable-alpha-plugins` failed exit status 1: Error: loading generator plugins: failed to load generator: unable to find plugin root - tried: ('<no value>'; homed in $KUSTOMIZE_PLUGIN_HOME), ('<no value>'; homed in $XDG_CONFIG_HOME), ('/.config/kustomize/plugin'; homed in default value of $XDG_CONFIG_HOME), ('/kustomize/plugin'; homed in home directory)


aws iam create-policy --policy-name letsencrypt-wildcard --policy-document file://letsencrypt-wildcard.json
LE_POLICY_ARN=$(aws iam list-policies --output json --query 'Policies[*].[PolicyName,Arn]' --output text | grep letsencrypt-wildcard | awk '{print $2}')\naws iam create-group --group-name letsencrypt-wildcard\naws iam attach-group-policy --policy-arn ${LE_POLICY_ARN} --group-name letsencrypt-wildcard\naws iam create-user --user-name letsencrypt-wildcard\naws iam add-user-to-group --user-name letsencrypt-wildcard --group-name letsencrypt-wildcard\naws iam create-access-key --user-name letsencrypt-wildcard
 oc create secret generic aws-route53-creds --from-literak=awsSecretAccessKey="rUB+ZJjrZHlJp0vYPxoIDz0uqNpPWM2dMw03cTxk" -n cert-manager\n