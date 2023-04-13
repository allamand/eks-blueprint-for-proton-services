# Repository for Sync AWS Proton Services in git

## Troubleshoot

Call Proton API

```bash
aws proton get-service-instance-sync-status --service-instance-name green --service-name dev-eks-green
aws proton get-service-instance-sync-status --service-instance-name pink --service-name dev-eks-pink
```

```bash
aws proton get-service-sync-blocker-summary --service-name dev-eks-blue
aws proton get-service-sync-blocker-summary --service-name dev-eks-blue --service-instance-name blue
aws proton get-service-sync-blocker-summary --service-name dev-eks-pink --service-instance-name pink

```

```json
aws proton get-service-sync-blocker-summary --service-name dev-eks-blue --service-instance-name blue
{
    "serviceSyncBlockerSummary": {
        "latestBlockers": [
            {
                "contexts": [
                    {
                        "key": "AUTOMATED",
                        "value": "Wed Apr 12 08:13:41 UTC 2023"
                    }
                ],
                "createdAt": "2023-04-12T08:13:41.489000+00:00",
                "createdReason": "Target arn:aws:proton:eu-west-1:382076407153:service/dev-eks-blue/service-instance/blue was modified at time Wed Apr 12 07:20:42 UTC 2023 by something besides ServiceSync. Disabling syncing to ensure we don't overwrite an important deployment.",
                "id": "2bddd721-46d2-41dd-b6d2-2b057c0f29c2",
                "status": "ACTIVE",
                "type": "AUTOMATED"
            }
        ],
        "serviceInstanceName": "blue",
        "serviceName": "dev-eks-blue"
    }
}
```

get the id and call

```bash
aws proton update-service-sync-blocker --id 2bddd721-46d2-41dd-b6d2-2b057c0f29c2 --resolved-reason "seb manually resolve conflict"
```