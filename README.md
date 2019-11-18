[![Actions Status](https://github.com/cemkiy/action-islack/workflows/Main/badge.svg?branch=master)](https://github.com/cemkiy/action-islack/actions)

# action-islack

You can send slack message easily. islack is supported slack attachments.
Detail info:  https://api.slack.com/docs/messages/builder

## Configurations

You sould set 'SLACK_WEBHOOK' variable to your repo secrets in settings page.
Detail info: [help.github.com/...](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets#creating-encrypted-secrets)

## Usage

Create a workflow and set a step like this.
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

islack has default output about your git event.
```sh
cemkiy/action-islack/Notification on push to master triggered by cemkiy (push)
```

If you set attachment fields, you should see advanced message in your slack. But default message is always sending.

## Advanced Usage

If you want show different messages in your workflow, use success and failure func.

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
