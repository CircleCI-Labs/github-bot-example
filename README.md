# GtiHub Bot Example
An example repo to show off inbound webhooks triggering based on issue comments. GitHub's issue comments are not granular enough
to just allow comments on PRs, so we need to do some additional filtering on CircleCI's side to determine if we should run a 
pipeline. 

This is accomplished by running a small docker job which will inspect the JSON payload GitHub sent. We will look for the following:

- If `AUTHOR_ASSOCIATION` is either `COLLABORATOR` or `MEMBER` or `OWNER` or `CONTRIBUTOR`
- If the comment was left on a PR and not just an issue
- If the comment contains the word `circleci`

If all 3 conditions are met, the pipeline will continue on to the normal pipeline. If not, the pipeline will fail and not continue.
