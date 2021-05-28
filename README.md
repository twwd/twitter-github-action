# Twitter GitHub Action

Tweets from a GitHub action workflow.

## Twitter Application Setup

You need a Twitter application to authenticate to the Twitter API and use it e.g. for sending tweets.

If you don't have already one, you can create in on [developer.twitter.com/apps](https://developer.twitter.com/apps). Then you should set the app permissions to _Read and Write_ and fetch the _consumer keys_ (API key and API secret key) plus the access token and secret for the user on which behalf the action should tweet.

## Secret Configuration

Store these tokens and keys as secrets in your repository, e.g. as
- `TWITTER_API_KEY` for the consumer API key,
- `TWITTER_API_SECRET_KEY` for the consumer API secret key,
- `TWITTER_ACCESS_TOKEN` for the user access token, and
- `TWITTER_ACCESS_TOKEN_SECRET` for the user secret.


## Usage

```yaml
- uses: twwd/twitter-github-action@v1
  with:
    twitter_api_key: ${{ secrets.TWITTER_API_KEY }}
    twitter_api_secret_key: ${{ secrets.TWITTER_API_SECRET_KEY }}
    twitter_access_token: ${{ secrets.TWITTER_ACCESS_TOKEN }}
    twitter_access_token_secret: ${{ secrets.TWITTER_ACCESS_TOKEN_SECRET }}
    tweet_body: 'The content of the tweet'
```

### Example Scenario: Tweet on Release

```yaml
name: "Tweet about release"
on:
  release:
    types: [ published ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Tweet
        uses: twwd/twitter-github-action@v1
        with:
          twitter_api_key: ${{ secrets.TWITTER_API_KEY }}
          twitter_api_secret_key: ${{ secrets.TWITTER_API_SECRET_KEY }}
          twitter_access_token: ${{ secrets.TWITTER_ACCESS_TOKEN }}
          twitter_access_token_secret: ${{ secrets.TWITTER_ACCESS_TOKEN_SECRET }}
          tweet_body: |
            We just released version ${{ github.event.release.tag_name }} of ${{ github.event.repo.name }} 🎉
            Check it out here ${{ github.event.release.html_url }}
```


