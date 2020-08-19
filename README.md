# React-Chatbot-Cum-NewsReaderApp 🌐

This is a news reader application with voice recognisation. I have used ALAN AI STUDIO for voice recognisation purpose.

## Special links :
<a href="https://alan.app/">Click here to learn more about Alan</a></br>
<a href="https://newsapi.org/">Click here for API Source</a>

## ALAN AI CODE :
```
// Use this sample to create your own voice commands
intent('What does this app do?', 'What can I do here?', p=>  {
    p.play('This is a react news application');
});

const API_KEY = 'f3c63772c01a4934a97c41ab1414852a';
let savedArticles = [];

// News by Source
intent('Give me the news from $(source* (.*))', (p) => {
    let NEWS_API_URL = `https://newsapi.org/v2/top-headlines?apiKey=${API_KEY}`;
    
    if(p.source.value) {
        NEWS_API_URL = `${NEWS_API_URL}&sources=${p.source.value.toLowerCase().split(" ").join('-')}`
    }
    
    api.request(NEWS_API_URL, (error, response, body) => {
        const { articles } = JSON.parse(body);
        
        if(!articles.length) {
            p.play('Sorry, please try searching news from a different source');
            return;
        }
        
        savedArticles = articles;
        
        p.play({ command: 'newHeadlines', articles});
        p.play(`Here are the (latest|recent) ${p.source.value}.`);
        
        p.play('Would you like me to read the headlines?');
        p.then(confirmation);
    });
})

//News by term
intent('what\'s up with $(term* (.*))', (p) => {
    let NEWS_API_URL = `https://newsapi.org/v2/everything?apiKey=${API_KEY}`;
    
    if(p.term.value) {
        NEWS_API_URL = `${NEWS_API_URL}&q=${p.term.value}`
    }
    
    api.request(NEWS_API_URL, (error, response, body) => {
        const { articles } = JSON.parse(body);
        
        if(!articles.length) {
            p.play('Sorry, please try searching for something else.');
            return;
        }
        
        savedArticles = articles;
        
        p.play({ command: 'newHeadlines', articles });
        p.play(`Here are the (latest|recent) articles on ${p.term.value}.`);
        
        p.play('Would you like me to read the headlines?');
        p.then(confirmation);
    });
})

// News by Categories
const CATEGORIES = ['business', 'entertainment', 'general', 'health', 'science', 'sports', 'technology'];
const CATEGORIES_INTENT = `${CATEGORIES.map((category) => `${category}~${category}`).join('|')}|`;

intent(`(show|what is|tell me|what's|what are|what're|read) (the|) (recent|latest|) $(N news|headlines) (in|about|on|) $(C~ ${CATEGORIES_INTENT})`,
  `(read|show|get|bring me|give me) (the|) (recent|latest) $(C~ ${CATEGORIES_INTENT}) $(N news|headlines)`, (p) => {
    let NEWS_API_URL = `https://newsapi.org/v2/top-headlines?apiKey=${API_KEY}`;
    
    if(p.C.value) {
        NEWS_API_URL = `${NEWS_API_URL}&category=${p.C.value}`
    }
    
    api.request(NEWS_API_URL, (error, response, body) => {
        const { articles } = JSON.parse(body);
        
        if(!articles.length) {
            p.play('Sorry, please try searching for a different category.');
            return;
        }
        
        savedArticles = articles;
        
        p.play({ command: 'newHeadlines', articles });
        
        if(p.C.value) {
            p.play(`Here are the (latest|recent) articles on ${p.C.value}.`);        
        } else {
            p.play(`Here are the (latest|recent) news`);   
        }
        
        p.play('Would you like me to read the headlines?');
        p.then(confirmation);
    });
});

const confirmation = context(() => {
    intent('yes', async (p) => {
        for(let i = 0; i < savedArticles.length; i++){
            p.play({ command: 'highlight', article: savedArticles[i]});
            p.play(`${savedArticles[i].title}`);
        }
    })
    
    intent('no', (p) => {
        p.play('Sure, sounds good to me.')
    })
})

intent('open (the|) (article|) (number|) $(number* (.*))', (p) => {
    if(p.number.value) {
        p.play({ command:'open', number: p.number.value, articles: savedArticles})
    }
})

intent('(go|) back', (p) => {
    p.play('Sure, going back');
    p.play({ command: 'newHeadlines', articles: []})
})
```

## 📲 Connect with me on social media 
<p align="left">
  <a target="_blank"href="https://www.linkedin.com/in/santanu-biswas-1482591a7/"><img src="https://img.shields.io/badge/linkedin-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white" /></a>&nbsp;&nbsp;&nbsp;&nbsp;<br/>
  <a target="_blank"href="https://www.facebook.com/Neil7rockzz"><img src="https://img.shields.io/badge/-FACEBOOK-0066ff?&style=for-the-badge&logo=facebook&logoColor=white" /></a>&nbsp;&nbsp;&nbsp;&nbsp;<br/>
  <a target="_blank"href="https://github.com/SantanuxD"><img src="https://img.shields.io/badge/GitHub-black.svg?&style=for-the-badge&logo=github&logoColor=white" /></a>&nbsp;&nbsp;&nbsp;&nbsp;<br/>
  <a target="_blank"href="https://www.instagram.com/_.santanubiswas._/"><img src="https://img.shields.io/badge/-INSTAGRAM-cc0099?&style=for-the-badge&logo=instagram&logoColor=white" /></a>&nbsp;&nbsp;&nbsp;&nbsp;<br/>
  <a href="https://twitter.com/Santanu97990818"><img src="https://img.shields.io/badge/-TWITTER-1ca0f1?&style=for-the-badge&logo=twitter&logoColor=white"/></a>&nbsp;&nbsp;&nbsp;&nbsp;<br/>
  <a href="mailto:neil16biswas@gmail.com"><img src="https://img.shields.io/badge/gmail-%23D14836.svg?&style=for-the-badge&logo=gmail&logoColor=white" /></a>&nbsp;&nbsp;&nbsp;&nbsp;
  
</p>

Give a star 🌟 if you like it.

