# WebHook

## 1. Outgoing WebHook

Note: Webhook to Slack and Rocket.Chat does not require adding anything to URL. Discord requires adding `/slack` to end of URL so that it works.

<img src="https://wekan.github.io/outgoing-webhook-discord.gif" alt="Outgoing Webhook to Discord" />

1. Add Webhook to Discord

2. On Wekan board, click 3 lines "hamburger" menu / Outgoing Webhooks.

3. Add /slack to end of your Discord Webhook URL and Save URL, like this: 

```
https://discordapp.com/api/webhooks/12345/abcde/slack
```

Wekan Outgoing Webhook URLs are in Slack/Rocket.Chat/Discord format.

Note: Not all Wekan activities create Outgoing Webhook events. Missing activities [have been added](https://github.com/wekan/wekan/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+webhook) to [Wekan Roadmap](https://github.com/wekan/wekan/projects/2). If you find some activity that does not yet have GitHub issue about it, please add new GitHub issue.

Wekan uses this type of JSON when sending to Outgoing Webhook:
https://github.com/wekan/wekan/wiki/Webhook-data

Discord supports incoming webhooks in different formats, like GitHub, Slack, etc. The incoming format needs to be specified by adding webhook format to end of URL.
https://discordapp.com/developers/docs/resources/webhook#execute-slackcompatible-webhook

Wekan generated webhooks are Slack compatible. Discord does not know anything about Wekan, Rocket.Chat, and other apps that produce Slack compatible Outgoing Webhook format. But using any other format like GitHub etc does not work, because Wekan Outgoing Webhooks are not in that format.

When making Wekan Outgoing Webhook to Rocket.Chat and Slack, there is no need to add anything to Webhook URL when those that is added to Wekan board. Discord in this case has decided to implement multiple Incoming Webhook formats and require specifying format in URL.

## 2. Outgoing Webhook to Discord

Note: Webhook to Slack and Rocket.Chat does not require adding anything to URL. Discord requires adding `/slack` to end of URL so that it works.

<img src="https://wekan.github.io/outgoing-webhook-discord.gif" alt="Outgoing Webhook to Discord" />

1. Add Webhook to Discord

2. On Wekan board, click 3 lines "hamburger" menu / Outgoing Webhooks.

3. Add /slack to end of your Discord Webhook URL and Save URL, like this: 

```
https://discordapp.com/api/webhooks/12345/abcde/slack
```

Wekan Outgoing Webhook URLs are in Slack/Rocket.Chat/Discord format.

Note: Not all Wekan activities create Outgoing Webhook events. Missing activities [have been added](https://github.com/wekan/wekan/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+webhook) to [Wekan Roadmap](https://github.com/wekan/wekan/projects/2). If you find some activity that does not yet have GitHub issue about it, please add new GitHub issue.

Wekan uses this type of JSON when sending to Outgoing Webhook:
https://github.com/wekan/wekan/wiki/Webhook-data

Discord supports incoming webhooks in different formats, like GitHub, Slack, etc. The incoming format needs to be specified by adding webhook format to end of URL.
https://discordapp.com/developers/docs/resources/webhook#execute-slackcompatible-webhook

Wekan generated webhooks are Slack compatible. Discord does not know anything about Wekan, Rocket.Chat, and other apps that produce Slack compatible Outgoing Webhook format. But using any other format like GitHub etc does not work, because Wekan Outgoing Webhooks are not in that format.

When making Wekan Outgoing Webhook to Rocket.Chat and Slack, there is no need to add anything to Webhook URL when those that is added to Wekan board. Discord in this case has decided to implement multiple Incoming Webhook formats and require specifying format in URL.

## 3. Webhook and Let's Encrypt's

Because NodeJS uses an [hardcoded list of certificates](https://github.com/nodejs/node/issues/4175) if you deploy a site (receiving the webhook from wekan) behind a reverse proxy on https with a Let's Encrypt certificate you may have a problem: Let's Encrypt's CA is not recognized. The correct answer is [here](https://stackoverflow.com/questions/29283040/how-to-add-custom-certificate-authority-ca-to-nodejs/47160447#47160447).

* Download the Let’s Encrypt Authority X3 (IdenTrust cross-signed) from [here](https://letsencrypt.org/certificates/)
```sh
cd /etc/ssl/certs
wget https://letsencrypt.org/certs/lets-encrypt-x3-cross-signed.pem.txt -O lets-encrypt-x3-cross-signed.pem
```

* Now start the application with 
```sh
NODE_EXTRA_CA_CERTS=/etc/ssl/certs/lets-encrypt-x3-cross-signed.pem node main.js
```

## 4. Webhook data

When a webhook is activated it sends the related information within the POST request body.

### Card creation

```
{
  text: '{{wekan-username}} added "{{card-title}}" to "{{list-name}}"\nhttp://{{wekan-host}}/b/{{board-id}}/{{board-name}}/{{card-id}}',
  cardId: '{{card-id}}',
  listId: '{{list-id}}',
  boardId: '{{board-id}}',
  user: '{{wekan-username}}',
  card: '{{card-title}}',
  description: 'act-createCard'
}
```

### Card archival

```
{
  text: '{{wekan-username}} archived "{{card-title}}"\nhttp://{{wekan-host}}/b/{{board-id}}/{{board-name}}/{{card-id}}',
  cardId: '{{card-id}}',
  listId: '{{list-id}}',
  boardId: '{{board-id}}',
  user: '{{wekan-username}}',
  card: '{{card-title}}',
  description: 'act-archivedCard'
}
```

### Comment creation

```
{
  text: '{{wekan-username}} commented on "{{card-title}}": "{{comment-body}}"\nhttp://{{wekan-host}}/b/{{board-id}}/{{board-name}}/{{card-id}}',
  cardId: '{{card-id}}',
  boardId: '{{board-id}}',
  comment: '{{comment-body}}',
  user: '{{wekan-username}}',
  card: '{{card-title}}',
  description: 'act-addComment'
}
```

### Card move

```
{
  text: '{{wekan-username}} moved "{{card-title}}" from "{{old-list-name}}" to "{{new-list-name}}"\nhttp://{{wekan-host}}/b/{{board-id}}/{{board-name}}/{{card-id}}',
  cardId: '{{card-id}}',
  listId: '{{new-list-id}}',
  oldListId: '{{old-list-id}}',
  boardId: '{{board-id}}',
  user: '{{wekan-username}}',
  card: '{{card-title}}',
  description: 'act-moveCard'
}
```


