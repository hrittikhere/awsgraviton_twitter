## Inspiration
Most people go to any social media to find topics that interest them. With time noise kicks in, and viewers can't find tweets they want to see. 

![Katy](https://raw.githubusercontent.com/hrittikhere/awsgraviton_twitter/main/static/katy_aws.png)

Ref: [Tweet from KatyCodes]( https://twitter.com/KatyCodesStuff/status/1443463354564194309)


Other than that, it might be the case someone uses Twitter to look at what's going on daily in some specific field. As for my work, I need to see what content is being circulated on Twitter and what's a trend in Kubernetes communities. My Bot helps other followers and me with the purpose of being updated with Kubernetes.

___"Hi Hrittik, The Bot is very useful. It gives me relevant content for me to share and gain new connections. I primarily use twitter to spread the word on my opensource project "kube-fledged". And definitely your Bot helps in this goal. Thanks, Senthil. 😀"___ - _@senthilrch, Principal SW Engineer @ericsson_



## What it does
My Bot Fetches the latest tweet with the words Kubernetes and some other secondary words without being dependent on hashtags every 4 hours and then RTs the tweets that aren't already posted before. 
It's periodic by intention because I like to open Twitter and get updated at a specific time with 50 tweets and not 200 at the end of the day. People like the periodic nature and the no #tag approach nature. 

## How we built it
The Bot is built using python with the help of the tweepy,  socks and other libraries. It's hosted on GitHub. The code is pulled from the remote repository periodically without you needing to access the machine. Any time you update the code on github, it's pulled via cron jobs in 1 min, and the updated code becomes the backend.
### Secure Run
So, to run the Bot we need the libraries, Twitter tokens and the code. We take care of the code in the previous stage and the tokens are already securely uploaded on the VM's code repository. We protect the access tokens by keeping the file (tokens.py) in .gitignore. 
With the code and access tokens taken care of, the run function works similarly to how the code is remotely pulled, i.e., via cron jobs on Graviton X2gD (Lowest $/GIB of RAM) every four hours.

![Architecture](https://raw.githubusercontent.com/hrittikhere/awsgraviton_twitter/main/static/ec2.png)


## Challenges we ran into
The First challenge was building something that just doesn't RTs hashtags. This is important because the promotions use hashtags more than ordinary people. Queries often go unnoticed because they missed the hashtag part. A lot of time was invested writing compact code and focusing on strings rather than hashtags. 
I focused on creating a compact base and code that's small instead of very big code and hard for people to understand. I used a lot of function calls to achieve this. 

Next, the big challenge was to deploy it, but it wasn't possible via GitHub actions because of the limited number of minutes per month. Self hosted runner was an option but GitHub Runners aren't the reliable and sometimes go down and you're bombarded with notification for Failed Pipeline. Another disadvantage of the approach is [python package isn't available for the ARM architecture currently](https://downloads.python.org/pypy/versions.json). I experimented with Docker because of Graviton, but it wasn't that efficient when I thought of the future plans and accumulated feedback. 

So, the cron solution works excellent currently, and it can scale to more bots. More details about it  in the lateral sections.
```
0 */4 * * * python3 /home/ubuntu/austin_castel/my_twitter_bot.py >> /home/ubuntu/log/log.txt
```

## Accomplishments that we're proud of
1.	Participating in my first hackathon and submitting a project in the 'hacker' way
2.	Getting to 100+ followers quickly in a matter of few weeks and receiving lovely feedbacks from followers.
3.	Generating a system on AWS EC2 that can scale to more bots and become cost efficient with the economy of scale. 
4.	Learning Linux commands, crontabs and excellent python libraries like Tweepy.


## What we learned
There's a huge demand for targeted bots. Like one of the followers puts it:


___"Your Bot is awesome Thumbs upClapping hands sign
 It helped me focussing only on the content I want to see i.e Kubernetes. If possible do same for terraform. That's the only feedback I have for now. But I will surely give more over the time. Thanks"__ - @SagarJadhv23, Software Engineer IBM_

Also, cron jobs on Linux are more potent than it seems at the surface. I enjoyed learning Linux and empowering my application on Linux. 
Also, thanks to AWS for the credits to experiment with cloud. I learned how to SSH on a VM using private keys, deploy software there, and treat it as my cloud computer. I am also looking to get an AWS  practitioner certification for myself in future :D 

## What's next for AWS Graviton, GitHub and Twitter Bot
The plan for the Bot would be to create replicas for different niches like Terraform and AWS. But, I need to refine the algorithm a bit to not RT content with similar hashtags. I have plans to implement that in a couple of weeks.
The best part of using Graviton EC2 is that I don't need to deploy more VMs, even if I have ten bots focusing on 10 niches. It's just a line of code on crontab, and my Bot would run and help more people. So, I plan to scale the number of my bots, and if I win, Graviton is very compute-intensive at a low cost (Eg: X2gD with Lowest $/GIB of RAM) and it will support me to scale.
  
