[![Actions Status](https://github.com/cemkiy/action-islack/workflows/Main/badge.svg?branch=master)](https://github.com/cemkiy/action-islack/actions)

# Slack - Github Action

A [Github Action](https://github.com/features/actions) to send a message to a Slack channel that supports attachments like images.

## Configuration

You must set `SLACK_WEBHOOK` environment value in settings page of your repository in order to use without any problem. Please [see here](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets#creating-encrypted-secrets) to learn how to do it if you don't know already.

## Usage

Create a workflow, set a step that uses this action and don't forget to specify `SLACK_WEBHOOK` environment value.

```yaml
name: Notification on push

on:
  push:
    branches:
    - master

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Slack notification
      env:
        SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK }}
      uses: cemkiy/action-islack@master
      with:
        # requirements fields for slack
        channel: '#channel-name'
        icon_url: 'slack user icon url'
        username: 'slack username'
        # attachment fields(not required)
        fallback: 'Required plain-text summary of the attachment.'
        color: '#36a64f'
        pretext: 'Optional text that appears above the attachment block'
        author_name: 'John Doe'
        author_link: 'http://jdoe.com/me/'
        author_icon: 'http://imageurl.com/icons/icon.jpg'
        title: 'Slack API Documentation'
        title_link: 'https://api.slack.com/'
        text: 'Optional text that appears within the attachment'
        image_url: 'http://my-website.com/path/to/image.jpg'
        thumb_url: 'http://example.com/path/to/thumb.png'
        footer: 'Slack API'
        footer_icon: 'https://platform.slack-edge.com/img/default_application_icon.png'
```

## Output

Default output if you've not set any attachment will look like this.

```sh
cemkiy/action-islack/Notification on push to master triggered by cemkiy (push)
```

If you've set an attachment, you should see it in addition to default message.

## Advanced Usage

If you want to show different messages based on succes or failure of previous steps in your workflow, use success and failure functions.

```yaml
- name: Slack notification Failure
  if: failure()
  env:
    SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK }}
  uses: cemkiy/action-islack@master
  with:
    channel: '#channel-name'
    icon_url: 'slack user icon url'
    username: 'slack username'
    image_url: 'http://my-website.com/path/to/failure.jpg'

- name: Slack notification Success
  if: success()
  env:
    SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK }}
  uses: cemkiy/action-islack@master
  with:
    channel: '#channel-name'
    icon_url: 'slack user icon url'
    username: 'slack username'
    image_url: 'http://my-website.com/path/to/success.jpg'
```

## Contributing

Please see [API documentation](https://api.slack.com/docs/messages/builder) in addition to source code in this repository.
