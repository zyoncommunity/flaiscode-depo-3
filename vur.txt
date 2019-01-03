const Discord = require('discord.js');

exports.run = async (client, msg, args) => {
   var sans = ["11", "15", "20", "24", "28", "31", "39", "45", "49", "54", "58", "63", "67", "77", "73", "84", "80", "83", "96", "94", "99"];
    var sonuc = sans[Math.floor((Math.random() * sans.length))]
  const vurresim = new Discord.RichEmbed()
  .setImage('http://3.bp.blogspot.com/-kh5On-pZMkM/UfaITUTRR_I/AAAAAAAAA70/piGjpI38tB0/s1600/boxing-machine-practice-attempt-fail.gif')
  .setColor('RANDOM')
  msg.channel.send('Vuruyorum! :boxing_glove:')
.then(nmsg => nmsg.edit('Vuruyorum! :boxing_glove:'))
.then(nmsg => nmsg.edit('Vuruyorum! :boxing_glove:'))
.then(nmsg => nmsg.edit('Vuruyorum! :boxing_glove:'))
.then(nmsg => nmsg.edit(vurresim))
  .then(nmsg => nmsg.edit(vurresim))
.then(nmsg => nmsg.edit('Vurdun!'))
    .then(nmsg => nmsg.edit('Vurdun!'))
    .then(nmsg => nmsg.edit('Vurdun!'))
.then(nmsg => nmsg.edit('Vurdun!'))
   await msg.channel.send(`${msg.author} Skorun: **${sonuc}**`)
 
   }   


exports.conf = {
  enabled: true,
  guildOnly: true,
  aliases: [],
  permLevel: 0
};

exports.help = {
  name: 'vur',
  description: '',
  usage: ''
};