# Provision ALB Listener Rule

## Description

This GitHub Action provisions an ALB listener rule for an Elastic Load Balancer (ELB). It checks if the rule already exists and creates a new rule if it doesn't. The action ensures that the specified hostname is associated with the ALB listener rule and forwards traffic to the specified target group.

## Inputs

| Name                  | Description                                                  | Required | Default                  |
| --------------------- | ------------------------------------------------------------ | -------- | ------------------------ |
| `elbName`             | The name of the Elastic Load Balancer (ELB).                | ✔        | `ecs-modular-monolith`   |
| `elbListenerHostname` | The hostname for the ALB listener rule.                      | ✔        |                          |
| `targetGroupArn`      | The ARN of the target group to which the traffic should be forwarded. | ✔        |                          |

## Outputs

This action doesn't have any outputs.

## Example Usage

```yaml
jobs:
  provision-alb-listener-rule:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Provision ALB Listener Rule
        id: alb-rule
        uses: caring/provision-alb-listener-rule@v1.0.0
        with:
          elbName: ecs-modular-monolith
          elbListenerHostname: ecs-modular-monolith
          targetGroupArn: arn:aws:elasticloadbalancing:us-west-2:123456789012:targetgroup/example-target-group/abcdef1234567890

      - name: Print Existing ALB Listener Rules
        run: |
          echo "Existing ALB listener rules:"
          echo "${{ steps.alb-rule.outputs.existingRules }}"
```

This action will provision an ALB listener rule for the specified ELB, associated with the provided hostname and target group ARN. It can be used in your workflow to ensure proper routing of traffic to the desired target group.

## License

This project is licensed under the [MIT License](LICENSE).

## Author

Written by the DevOps Team.