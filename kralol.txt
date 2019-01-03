client.on("message", async message => {
  var user = message.mentions.users.first() || message.author;
    if (message.content.toLowerCase() === prefix + "kralol") {
        var user = message.mentions.users.first() || message.author;
        if (!message.guild) user = message.author;

        message.channel.send(":loudspeaker: | **Kralol** Çerçevesi Uygulanıyor!").then(m => m.delete(1000));
        await message.channel.send(`**${message.author.tag}** artık kral oldun!`)
        Jimp.read(user.avatarURL, (err, image) => {
            image.resize(310, 325)
            Jimp.read("https://cdn.discordapp.com/attachments/508207771741716480/508210101048573955/kral.png", (err, avatar) => {
                avatar.resize(310, 325)
                image.composite(avatar, 2, 0).write(`./img/snip/${client.user.id}-${user.id}.png`);
                setTimeout(function() {
                    message.channel.send(new Discord.Attachment(`./img/snip/${client.user.id}-${user.id}.png`));
                }, 1000);
            });

        });
    }
});