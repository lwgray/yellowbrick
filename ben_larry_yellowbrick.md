# 📝 Notes

Jun 25, 2025

## Meeting Jun 25, 2025 at 19:37 CDT

Meeting records [Transcript](?tab=t.2mjl1v5ps79u) [Recording](https://drive.google.com/file/d/1GKFlKC9umTJ9BCLepjrrYd7TO0-wugbU/view?usp=drive_web)

### Summary

Lawrence Gray and Benjamin Bengfort addressed incompatibility issues and the need to move Yellow Brick to its own organization, noting open pull requests. Benjamin Bengfort created a new environment, updated dependencies resulting in matplotlib upgrade, managed baseline images for tests, and encountered failures possibly due to random number generation and outdated test dependencies. They discussed image diffing improvements, considered Python version upgrades for testing, and Benjamin Bengfort identified several specific errors related to dependency updates and backward compatibility, suggesting potential minimum version bumps for Matplotlib and NumPy while cautioning about major version jumps in Pandas.

### Details

* **Starting Point and Issue Identification** Lawrence Gray and Benjamin Bengfort agreed to start by addressing the incompatibility issue Jake previously identified. Benjamin Bengfort inquired about the scikit-learn version ([00:00:00](#00:00:00)) and expressed a desire to move Yellow Brick into its own organization. They noted the existence of 14 open pull requests ([00:02:12](#00:02:12)).

* **Environment Setup and Dependency Management** Benjamin Bengfort created a new virtual environment named "yb\_depths" with Python 3.12.6. They then used \`pip install\` with the existing \`requirements.txt\` file, which specified greater than version requirements, to install the latest versions of dependencies ([00:04:17](#00:04:17)). This resulted in an upgrade of matplotlib to version 3.10 ([00:06:32](#00:06:32)).

* **Test Execution and Initial Failures** Upon running \`pytest\`, Benjamin Bengfort anticipated a large number of failures ([00:07:38](#00:07:38)). They identified an issue in the \`requirements.txt\` file where matplotlib was listed with a lower than acceptable version and removed it ([00:09:23](#00:09:23)). Subsequent test runs showed some tests passing, but many image comparison failures occurred ([00:12:52](#00:12:52)).

* **Baseline Image Management** Benjamin Bengfort explained the process of managing baseline images for testing, involving "actual images" generated during test runs and "baseline images" for comparison. They used a script (\`python \-m tests.images\`) to manage these images ([00:21:31](#00:21:31)). Due to a large number of failures, Benjamin Bengfort deleted all existing baseline images to reset ([00:25:32](#00:25:32)).

* **Test Failures and Random Number Generation** Lawrence Gray mentioned that some test failures might be due to changes in the random number generation, causing slight discrepancies in generated numbers that affect comparisons. Benjamin Bengfort considered using an approximation method to handle these variations ([00:28:15](#00:28:15)).

* **Updating Test Dependencies** Benjamin Bengfort emphasized the importance of updating test dependencies to match the versions used to generate the new baseline images. They used a custom script named "requires" to update these dependencies in the \`test\_requirements.txt\` file ([00:30:01](#00:30:01)). Optional dependencies like catboost were also considered ([00:31:44](#00:31:44)).

* **Further Testing and Potential Issues** After updating dependencies and syncing baseline images, Benjamin Bengfort anticipated needing to re-sync the images again due to potential skips caused by missing optional dependencies initially ([00:35:38](#00:35:38)). An initial test run after these updates showed a significant reduction in the number of failures ([00:43:45](#00:43:45)).

* **Merge Conflicts and Code Review** Benjamin Bengfort encountered merge conflicts and used a "resolve all conflicts to current" approach with caution, recognizing the need to review the diffs for any unintended changes across the 331 changed files. They noted that data-only changes are usually acceptable ([00:46:11](#00:46:11)).

* **Image Diffing and Future Improvements** Lawrence Gray and Benjamin Bengfort discussed the image diffing process, acknowledging it as a good idea that needs further tuning, specifically mentioning that the RMSSE method might not be sufficient. They suggested exploring better algorithms for image comparison as a potential improvement for future upgrades ([00:49:57](#00:49:57)). Benjamin Bengfort spot-checked several image differences, noting that visually similar images were being flagged as different, possibly due to random number generation variations ([00:51:35](#00:51:35)).

* **Python Version Upgrade for Testing** Benjamin Bengfort proposed upgrading the Python versions used for testing from 3.8 and 3.9 to later versions like 3.11 and 3.12. This was prompted by errors indicating missing distributions for certain packages with older Python versions ([00:54:34](#00:54:34)). Benjamin Bengfort then updated the CI configuration (\`CI.yaml\`) and the \`setup.py\` file to reflect these new Python versions for testing and the minimum required Python version for Yellow Brick ([00:58:12](#00:58:12)).

* **Linting Failure and Test Status** Benjamin Bengfort reported that linting failed due to a missing pi test spec, but all other Python tests are running. They also mentioned uncertainty about why Anaconda is not working and stated that the current focus is on identifying and resolving these issues ([01:00:53](#01:00:53)).

* **Branch Management and Error Identification** Lawrence Gray confirmed that Benjamin Bengfort is working in a branch and offered to take over to fix the remaining errors. Benjamin Bengfort had already pushed the branch and identified several exceptions, including a reax pattern mismatch, an assertion error, and an "artist lists object has no attribute remove" error ([01:00:53](#01:00:53)).

* **Backward Compatibility and Dependency Updates** Benjamin Bengfort and Lawrence Gray discussed the "artist lists object has no attribute remove" error, noting it's due to the remove method being moved. They considered the implications for backward compatibility and the decision-making process for updating dependencies, such as Matplotlib. Benjamin Bengfort suggested that if a minimum version update involves a very recent version or if a package has a history of reverting changes, they are less inclined to do so ([01:02:54](#01:02:54)). However, if a version has been stable for a significant period (e.g., over a year in the case of one Matplotlib dependency), or if it resolves multiple issues, then upgrading the minimum dependency is acceptable ([01:04:01](#01:04:01)) ([01:06:40](#01:06:40)).

* **Ideal Update Frequency and Dependency Management** Benjamin Bengfort described an ideal scenario where frequent updates to Yellowbrick would necessitate continuous upgrades of its dependencies, thereby reducing concerns about long-term backward compatibility ([01:04:01](#01:04:01)). They highlighted the challenges of managing dependencies like Matplotlib and scikit-learn, emphasizing the desire to minimize the number of dependencies in library code ([01:05:19](#01:05:19)).

* **Specific Errors and Version Updates** Benjamin Bengfort noted that while there are 43 issues, updating Matplotlib and NumPy alone could potentially resolve around 30 of them. They suggested potentially bumping the minimum versions of both Matplotlib and NumPy and indicated that changes would be needed for \`is\_classifier\`, \`is\_agressor\`, and \`is\_outlier\` checks due to some minor bugs ([01:05:19](#01:05:19)). Benjamin Bengfort advised Lawrence Gray to use their best judgment on version upgrades and to reach out on Slack for clarification ([01:06:40](#01:06:40)).

* **Pandas and Matplotlib Version Considerations** Benjamin Bengfort cautioned about significant version jumps, such as from Pandas 1 to Pandas 2, and the need to decide on library support ([01:06:40](#01:06:40)). They recalled a previous issue with a Matplotlib update that broke functionality, leading to a specific exclusion in the requirements. However, Benjamin Bengfort confirmed that the old 2.0.2 Matplotlib dependency can be removed, and the minimum version can be set to 3.4 or higher ([01:07:40](#01:07:40)).

* **Transition of Responsibility and Appreciation** Lawrence Gray stated they could take over from this point. Benjamin Bengfort offered further assistance via Slack. They both expressed appreciation for each other's work on maintaining the library ([01:07:40](#01:07:40)).

### Suggested next steps

- [ ] Lawrence Gray will work on the pushed branch to fix errors like reax pattern and assertion issues.

- [ ] Lawrence Gray will address the 'remove' attribute error in the artist lists object, considering backward compatibility.

- [ ] Lawrence Gray will decide on updating matplotlib and numpy versions, considering stability, backward compatibility, and will ping Benjamin Bengfort on Slack if unsure.

*You should review Gemini's notes to make sure they're accurate. [Get tips and learn how Gemini takes notes](https://support.google.com/meet/answer/14754931)*

*Please provide feedback about using Gemini to take notes in a [short survey.](https://google.qualtrics.com/jfe/form/SV_9vK3UZEaIQKKE7A?confid=kTWpK0eTQmnMFUfVs0fqDxIVOAIIigIgABgBCA)*

# 📖 Transcript

Jun 25, 2025

## Meeting Jun 25, 2025 at 19:37 CDT \- Transcript

### 00:00:00 {#00:00:00}

 
**Benjamin Bengfort:** you have consented to have yourself recorded.
**Lawrence Gray:** Yes, I agree.
**Benjamin Bengfort:** Just so you
**Lawrence Gray:** I'm being I am being forced to say this if anyone's listening.
**Benjamin Bengfort:** you're under duress.
**Lawrence Gray:** Uh so um I guess what do you where should we start? Um, uh, objective is to kind of get it maybe up to start from where Jake's last said that it was having incompatibility. Um, and just fix fix that issue and we use that as our kind of starting point. Um,
**Benjamin Bengfort:** Yeah. Okay. So, what version of scikitlearn is this?
**Lawrence Gray:** let's see.
**Benjamin Bengfort:** 170\.
**Lawrence Gray:** How's business going, man?
**Benjamin Bengfort:** We're struggling on as we do. Are you on a big monitor?
**Lawrence Gray:** Uh, not really. I have two small monitors.
**Benjamin Bengfort:** All right. Well, I don't want to share my whole screen with you. because that'll be tough. All right. Um Haven't made a commit since 2023\.
**Lawrence Gray:** Yeah, I guess I should just
**Benjamin Bengfort:** All right, let's see.
 
 

### 00:02:12 {#00:02:12}

 
**Benjamin Bengfort:** Can you see this? Okay.
**Lawrence Gray:** Let me see. Yep, I can see it.
**Benjamin Bengfort:** Okay. So, I guess the first thing that I would do is we've got to figure out where the compatibility issue is. So, really would love to move yellow brick into its own organization. Um, so he opened an issue, right? Oh, there's 14 pull requests open. Wow.
**Lawrence Gray:** No.
**Benjamin Bengfort:** Okay. So, 1.7.0. And then if we do what's the latest version of scikitlearn
**Lawrence Gray:** I that that's it, right? Second
**Benjamin Bengfort:** 17
**Lawrence Gray:** 1.7.0, right?
**Benjamin Bengfort:** I don't have any idea. So normally what I would do
**Lawrence Gray:** Oh,
**Benjamin Bengfort:** here
**Lawrence Gray:** the latest version. No, I don't know if that's
**Benjamin Bengfort:** so let me get a terminal going here. How do I do that in VS code?
**Lawrence Gray:** Yeah, it's 1.7.0. No.
**Benjamin Bengfort:** Okay. All right. I don't know if you can see my screen okay or not, but
 
 

### 00:04:17 {#00:04:17}

 
**Lawrence Gray:** Yeah, I can see.
**Benjamin Bengfort:** good. All right. So, what I'm going to do is Okay, so I have yellow brick. So I'm going to
**Lawrence Gray:** This is
**Benjamin Bengfort:** make a new virtual environment essentially move. Um, so let's call this y depths. Okay, so this is going to be Python 3.12.6. Hopefully that's okay.
**Lawrence Gray:** Yeah. Okay.
**Benjamin Bengfort:** uh echo YB depths. Okay. So then what I'm going to do here now is I'm just going to pip install the requirements.
**Lawrence Gray:** How's Jackie and the There's joy.
**Benjamin Bengfort:** They're doing well. Arena's in uh Maryland with the grandparents right now and Jackie's working at Scholarship America and Henry's doing cooking camp. How about you guys?
**Lawrence Gray:** It's going well. My son, he's in um video game camp. He's developing Roblox games and stuff like that. Um so he's learning Lua to program in Lua. So, uh, but, um, Roblox just came out with an MCP and so we can connect Claude directly to it and so he can just come up whatever games he wants to now.
 
 

### 00:06:32 {#00:06:32}

 
**Lawrence Gray:** So, he's really excited about that.
**Benjamin Bengfort:** That's awesome. Okay, so basically I've just installed the latest version of all the dependencies
**Lawrence Gray:** Okay.
**Benjamin Bengfort:** and you can see that I have mapplot lib 310 now which is higher than 33 and I've got scikitlearn 170 so that must be the latest version. Um
**Lawrence Gray:** Did you just when you pipped installed the requirements, did you do upgrade or or how did you go from what was in the requirements folder to the latest versions? I I missed something.
**Benjamin Bengfort:** uh so this is our requirements.txt right here.
**Lawrence Gray:** Mhm.
**Benjamin Bengfort:** And so I created a new virtual environment
**Lawrence Gray:** Uhhuh.
**Benjamin Bengfort:** and then I just pip install requirements and you can see these are all greater thans.
**Lawrence Gray:** Oh,
**Benjamin Bengfort:** So
**Lawrence Gray:** okay.
**Benjamin Bengfort:** because
**Lawrence Gray:** I
**Benjamin Bengfort:** it's
**Lawrence Gray:** didn't
**Benjamin Bengfort:** greater than it
**Lawrence Gray:** Yeah,
**Benjamin Bengfort:** just
**Lawrence Gray:** that's
**Benjamin Bengfort:** installs
**Lawrence Gray:** what
**Benjamin Bengfort:** the latest version.
**Lawrence Gray:** Okay. I didn't see that.
 
 

### 00:07:38 {#00:07:38}

 
**Lawrence Gray:** Yeah. Okay, cool.
**Benjamin Bengfort:** Yeah. Um so under test there equals but under under the default requirements are different. So now if we do pi test we guess we can see what's failing.
**Lawrence Gray:** Yeah, it's about to be a lot of stuff. Do you
**Benjamin Bengfort:** I need to do this.
**Lawrence Gray:** So, what are the types of things that uh that kind of have your curiosity at the moment? What are what's happening in in technology that you're really excited about? That's the one-year-old
**Benjamin Bengfort:** That's the one-year-old right you know, just trying to keep my head above water with the everything. How about you? What is this?
**Lawrence Gray:** Am I the Agent stuff I've been playing around a lot with. Um
**Benjamin Bengfort:** love to know what your definition of agentic is because people always say agentic to me and
**Lawrence Gray:** Yeah. Yeah.
**Benjamin Bengfort:** I
**Lawrence Gray:** I
**Benjamin Bengfort:** want to
**Lawrence Gray:** I
**Benjamin Bengfort:** know
**Lawrence Gray:** I
**Benjamin Bengfort:** what you're talking up.
 
 

### 00:09:23 {#00:09:23}

 
**Lawrence Gray:** mean when I think agentic uh being able to access services um external services uh that's it um not any coordination between agents or anything like that.
**Benjamin Bengfort:** Yeah, that one more time. I got distracted by this trace trace back.
**Lawrence Gray:** Oh, no. I'm just talking about having access to external services through like MCP specifically. No coordination between agents. No, you know, 20 agents all working together to solve a problem kind of stuff. No, it's very limited. And the problem I'm trying to solve is uh building a project manager like project coordination uh agent that monitors and kind of coordinates other workers that are doing jobs. That's the toy thing I've been playing around with.
**Benjamin Bengfort:** All right. This is the problem right here. This is one problem. So I don't even know why we have this in there because map plot lib can't be lower than 150\. So, I don't even know why that's there. So, let's get rid of that. Okay. requires Mattplot lib.
 
 

### 00:12:52 {#00:12:52}

 
**Lawrence Gray:** Why did someone use a
**Benjamin Bengfort:** All All right. Now,
**Lawrence Gray:** that that bother bother me so much?
**Benjamin Bengfort:** let's do that. Uh, all right. Uh oh. Oh my god, it's everywhere. Okay, this is in wreck mod. So, same thing here again. Ways to make this shorter. So I'll make this that which probably is what we should have done in the first place. Hey, look at that. There's some test passing. That's good news. It's not all bad. A lot are failing, but at least some are passing. Okay. Sorry. Uh, yes. MCP everyone is uh loving. I'm actually so I'm working on a project called Honu DB which is a replicated database um and it will expose an MCP server but it's like it's a versioned document database that can also keep like vectors
**Lawrence Gray:** Mhm.
**Benjamin Bengfort:** indexed on top of it. And so we're using that in one of our projects that we're doing, but I'm working on on building that database out.
 
 

### 00:15:51

 
**Benjamin Bengfort:** So that's kind of my main focus right now.
**Lawrence Gray:** I just new job. Only thing I do is I basically just teach. Uh,
**Benjamin Bengfort:** Oh, so you are so you found a full-time job.
**Lawrence Gray:** yep.
**Benjamin Bengfort:** Great. What are you doing?
**Lawrence Gray:** working at a subsidiary of
**Benjamin Bengfort:** Very
**Lawrence Gray:** deer that builds autonomous tractors and lawnmowers and construction equipment. And so,
**Benjamin Bengfort:** cool.
**Lawrence Gray:** but uh I actually work with John Deere mostly um educating their engineers on using machine learning uh in their projects. So there's been a big push to get ML and um incorporated into all their work across the globe. And so we have like this mentorship program where they come in, they get basic training uh in machine learning and then they um they get they they have to apply to this program with a project, actual project that's supposed to go uh that's supposed to go live, like a live project that's going to go into a product and they spend a year working on it.
 
 

### 00:17:09

 
**Lawrence Gray:** And so uh we get about a hundred applicants and we over the entire year we just get them to go to actually and their work ends up going out into the field. Like it's pretty intense training. So but they put a lot of effort into doing this. We've been training people from Brazil to Germany like all and I get to teach some of the cool CBML stuff that I like. Um, and just trying to make it. It was pretty Blue River Technology who I worked for. Um, they were bought by John Deere 8 years ago because they had developed some pretty cool autonomous tractor stuff and um and did this technology called C and spray where you you have you actually pull the sprayer behind a behind a device, a vehicle and it sprays weeds like hyperfocused on just weeds in the field and it cut down herbicide use by like 80% on a on a field um with just some simple CV. You know, they had to work out the mechanics of how you get millisecond like spray times and stuff stuff like that and it hitting things while it's moving, but they figured it out.
 
 

### 00:18:39

 
**Lawrence Gray:** Um but uh they have a lot of good technology but I'm just there to really and also educate their the engineers there on the latest not only just educating people that won't that won't use it in a project with deer but also educate the the engineers the AI engineers on the latest technology that's out and bringing in best practices and stuff like that. So I reason I'm looking at a lot of the A genxic stuff is because they want to start incorporating more and more uh AI development tools and they the biggest fear they see is that there's a produ initial production loss uh when they're incorporating these tools like people don't aren't really like effective at first when they're using them and so they're trying to figure out a way to you know introduce use these tools in a way so that people can be effective as fast as possible. Um, but they want to incorporate them. So there's a big push now is to for me to go get training on best practices and using all these tools so that we can come back and train the entire force to be incorporating you know everyone because at a big organization like for them to just say we want to use you know cursor is a big deal right um so and they didn't even get cursor they wanted cursor and They had to use uh wind
 
 

### 00:20:14

 
**Lawrence Gray:** surf and co and and co-pilot and they wanted to use claude like they wanted claw so badly and the CTO couldn't get John Deere to agree to it. So
**Benjamin Bengfort:** Funny.
**Lawrence Gray:** So as far as Yeah. But so I'm actually looking forward to that because um so it's cool and I get to teach and uh continue teaching at Georgetown without issue and do other stuff that I want to do and the pay pay is more than I was getting paid before and
**Benjamin Bengfort:** Oh,
**Lawrence Gray:** the
**Benjamin Bengfort:** good.
**Lawrence Gray:** benefits are even better.
**Benjamin Bengfort:** Well, nice.
**Lawrence Gray:** Yeah.
**Benjamin Bengfort:** All right. Um, okay. So, we're at the step that I think that you wanted to record.
**Lawrence Gray:** Yeah.
**Benjamin Bengfort:** So, like now that I've um now that I've um fixed all like the errors because like now like things weren't importing that you know used to be there before and I so I manually fixed all those errors. Um there wasn't really a method to them except like looking
**Lawrence Gray:** Yeah.
 
 

### 00:21:31 {#00:21:31}

 
**Benjamin Bengfort:** at them and figuring out what was the best
**Lawrence Gray:** Yeah,
**Benjamin Bengfort:** thing to do.
**Lawrence Gray:** most definitely.
**Benjamin Bengfort:** Um, but now when you're in this set and you run the test, you get all of these image comparison failures.
**Lawrence Gray:** Yeah.
**Benjamin Bengfort:** That's the one that you can take care of with the uh command. So you have to run the tests first. And then what happens is if you look in tests and actually I should check out make sure I'm on a different branch here. So if you look at tests, there's this actual images and baseline images. And so actual images is not committed, but those are the the images that were generated during the test framework
**Lawrence Gray:** Mhm.
**Benjamin Bengfort:** run. And then baseline images are the ones that they're comparing them against. And so what we have is we have a little script that will basically copy over all of the actual images into the baseline images.
**Lawrence Gray:** Yeah.
**Benjamin Bengfort:** And I think it's if you do python-m tests images you got spell python right?
 
 

### 00:22:43

 
**Benjamin Bengfort:** Yeah this is it. So python-m testim images. You can see it's utility to manage baseline images for comparison. So dur directory to move images from actual to baseline. So what if I do Oh, and basically what we did is we did this so that you could do individual directories,
**Lawrence Gray:** Mhm.
**Benjamin Bengfort:** but with something this big, we might as well just do them all. So I think if we do tests actual images base images. All right. How does this work? How does this work again?
**Lawrence Gray:** That's it. Do you want to No, you don't want to clear them.
**Benjamin Bengfort:** Wow. Let me just open up the code and see what I'm supposed to do here. Test. I'm sure we've documented how to do this, but It might be clear. Move all non-def images from actual to baseline. argus. So it might just be star python-m tests images.py Hi. Um uh
**Lawrence Gray:** Yeah, python-m testim images and then the the test that you want to run.
 
 

### 00:25:32 {#00:25:32}

 
**Lawrence Gray:** You might have to, like you said, the asterisk
**Benjamin Bengfort:** no module name tests images. because that Oh, there it goes. Just deleted All right. What does the reading say? We have a helper class. So, Python test regressor test my visualizer.py.
**Lawrence Gray:** Yeah, that's what I just read. Yeah.
**Benjamin Bengfort:** So,
**Lawrence Gray:** And Claire removes it.
**Benjamin Bengfort:** we need an all flag.
**Lawrence Gray:** I think you can use asterisks like you
**Benjamin Bengfort:** Uh, well, I did and I didn't do all of them. How about star star? Oh, that did a lot.
**Lawrence Gray:** Yeah, I think that did all of
**Benjamin Bengfort:** So I deleted all of them and then Test star and test star star star star. I don't know how deep I need to go here. All right. So now if we do do pi test, everything should fail with no baseline image, right? Because I just deleted them all. And deleting them all is just like I just because we're doing so many, I'm just trying to clean up and reset
 
 

### 00:28:15 {#00:28:15}

 
**Lawrence Gray:** Yeah, there's going to be a few where there was uh we hardcoded some some uh
**Benjamin Bengfort:** Yeah.
**Lawrence Gray:** some changes that are just just way that they generate random numbers now actually affects what the numbers should be because I went through a lot of this before and it was like
**Benjamin Bengfort:** Okay.
**Lawrence Gray:** oh man you know this was all randomly generated but they changed to random generation and they're off by a decimal like you know a thousandth of a decimal point or something now and they're they're different number completely different numbers
**Benjamin Bengfort:** And we're not using like a prox or something.
**Lawrence Gray:** I know there
**Benjamin Bengfort:** Well, we should use a prox. Or is
**Lawrence Gray:** yeah
**Benjamin Bengfort:** it like
**Lawrence Gray:** no
**Benjamin Bengfort:** the
**Lawrence Gray:** it was like I think we did use approx but it was still far enough off that you had to expand approxim the approximation of
**Benjamin Bengfort:** That's too bad.
**Lawrence Gray:** So I think some of those um this was back a while whenever I open up that Hana DB.
 
 

### 00:30:01 {#00:30:01}

 
**Lawrence Gray:** Is that Oh, it's by your lab.
**Benjamin Bengfort:** Yeah, it was originally a research paper that I wrote and now we're turning it into like a hopefully a production database. I forgot how long these tests take.
**Lawrence Gray:** Yeah.
**Benjamin Bengfort:** Holy moly. Okay. So, baseline image does not exist. That's what we were hoping for. And now without the \- C flag, we will sync them. And then I'm going to commit this first. Oh, and actually there's one important thing. So when you do this, you have to make sure that the test dependencies are also updated. So you can see how the test dependencies are hardcoded here.
**Lawrence Gray:** Mhm.
**Benjamin Bengfort:** You want to make sure that those are um also hardcoded for the version that you generated the images on. Otherwise, the test
**Lawrence Gray:** Oh,
**Benjamin Bengfort:** will fail
**Lawrence Gray:** yeah.
**Benjamin Bengfort:** when
**Lawrence Gray:** Yeah.
**Benjamin Bengfort:** you go to
**Lawrence Gray:** I got to pass.
**Benjamin Bengfort:** Yeah. So I'm I'm going to use a special script requires.
 
 

### 00:31:44 {#00:31:44}

 
**Benjamin Bengfort:** So you can see requires just um I have. So, it requires just a script I have on my computer. If you want it, it's on a gist, but you can see it just updates everything in place for me. It's a little bit better than pip freeze. Um,
**Lawrence Gray:** It's something you wrote or it's something some tool you just found.
**Benjamin Bengfort:** it's something I wrote.
**Lawrence Gray:** Okay.
**Benjamin Bengfort:** It's It's a real short script, you know. If you want it, just let me know. I'll send it to you. I send it. People use it all the time. All right, let's deal with these optional dependencies. two cat boost. This is probably a terrible idea, but we're doing it anyway. And then I'm also going to install requirements.
**Lawrence Gray:** Doc requirements.
**Benjamin Bengfort:** Let's do get checkout requirements. All right. NLTK pandas um mapap learn Okay. So, there I've updated all of these dependencies now. And I'm going to get rid of all this because it doesn't matter for what we're doing here.
 
 

### 00:35:38 {#00:35:38}

 
**Benjamin Bengfort:** Okay. All right. Okay, let's see what kind of mess we've caused. So, because I just did that, I probably will have to do another sync of the images because there were probably a bunch of tests that were skipped because we didn't have like pandas and numpy and that kind of thing installed. So, I probably have to once again sync the baseline images, but
**Lawrence Gray:** Yeah, feel free. This is going to take two minutes at least, so you can step away if you need to.
**Benjamin Bengfort:** Um, 1327\. What? Hold on.
**Lawrence Gray:** Did you just send me something?
**Benjamin Bengfort:** No.
**Lawrence Gray:** Okay.
**Benjamin Bengfort:** Oh yeah, it's just the automated get. I mean, it feels like more things have passed.
**Lawrence Gray:** Yeah, it did. That's what I was Maybe things just work now magically.
**Benjamin Bengfort:** I mean, it's never that easy that it's like you hope that everything that I just did takes care of like 80% of the issues and then you have to like clean up, you know, other little things here and there.
 
 

### 00:39:53

 
**Benjamin Bengfort:** I mean, the satellite things aren't failing, but
**Lawrence Gray:** Are you teaching much at Georgetown?
**Benjamin Bengfort:** No. How about you?
**Lawrence Gray:** A lot.
**Benjamin Bengfort:** Are teaching a lot?
**Lawrence Gray:** Huh?
**Benjamin Bengfort:** You are teaching a lot.
**Lawrence Gray:** Yeah, I am. And I'm developing courses. So, when I was when I was gamefully unemployed, I was definitely take taking teaching as much as I could possibly teach. And then I took on before I got this job, I took on some development work. And now I'm kind of on the hook for it where I'm super busy now and I still have to develop these courses.
**Benjamin Bengfort:** I know how that goes. I should have looked to see how many times we've test failed the last run, but of course I
**Lawrence Gray:** was
**Benjamin Bengfort:** did not.
**Lawrence Gray:** 135
**Benjamin Bengfort:** Was 135\.
**Lawrence Gray:** out of a thousand. So,
**Benjamin Bengfort:** Like I said, 80% honestly don't understand how I have merge conflicts. All right. So, let's say this goes down to 100\. Then what we're hoping for is that all 100 of those things are failing because of one thing and they're not failing.
 
 

### 00:42:13

 
**Lawrence Gray:** Yeah, this
**Benjamin Bengfort:** And I mean frankly it's usually like three or four things you know when you fix them you know you take broad swats of tests out every time you fix something. So you know like should raise warning you know well okay that's just you know maybe something's changed there but we'll see. My god these tests take forever to run. This is like the most tested package I have ever written.
**Lawrence Gray:** Yeah. Well, there it sat alone for three years, man. And it's still people are still using it.
**Benjamin Bengfort:** I'll take
**Lawrence Gray:** So
**Benjamin Bengfort:** it.
**Lawrence Gray:** this all that effort is definitely well like this package is brilliantly written like very well written and so um like it's the whenever I think about anything that I develop now it's kind of based on like how is this like project as a whole how was it constructed the thoughts that were put into it. The thoughts about how people contribute to it. The thoughts that how people, you know, are are part of it and the community and all of that kind of bases like my vision of how open source supposed to work like
 
 

### 00:43:45 {#00:43:45}

 
**Benjamin Bengfort:** Not good.
**Lawrence Gray:** at its best and how you learn like I tell people all the time, if you really want to develop your software skills, go work on an open source project, right? Go work on that. you're going have to you will figure out how things kind of work together and for the most part people are going to be nice. You're going to get to kind of get in there and solve bigger, you know, bigger problems than you would on your own. And like it really really really changed the way that I approach code like you know it
**Benjamin Bengfort:** Awesome.
**Lawrence Gray:** um so I'm a definitely a big advocate for this project and I sh everyone that I showed is like I've used that before. I've used it before.
**Benjamin Bengfort:** Yeah, I mean that is how I learned how to code was uh contributing to open source one of the ways. 46\.
**Lawrence Gray:** and that cut it by half. So
**Benjamin Bengfort:** It's more than that.
**Lawrence Gray:** yeah.
**Benjamin Bengfort:** Thousand pass. I don't know what this cat boost info is.
 
 

### 00:46:11 {#00:46:11}

 
**Benjamin Bengfort:** app boost info. Cat boost\_info. Oh, that's annoying. Snikes.
**Lawrence Gray:** What happened?
**Benjamin Bengfort:** I got merge conflicts. All right. How do you get merge all conflicts resolved to current? All right, I'm going to do some stuff that you should not do unless you're feeling really super confident.
**Lawrence Gray:** Have you ever known me to be super confident? That's not one of my trades.
**Benjamin Bengfort:** So this X hours, that's what I'm doing.
**Lawrence Gray:** Oh, yeah. I've I I've done that before.
**Benjamin Bengfort:** I want what I have in my directory. Dang it. All right. So that fixed those merge conflicts sort of. So you know I guess kind of the thing we have like 331 files changed now. So like you do want to just kind of like look at the diffs and make sure that like nothing crazy has happened. You know what I mean? And like if there's data and like then it's usually fine, right? I mean, I'm going through these right now and they don't really look all that meaningfully different to me to be honest.
 
 

### 00:49:57 {#00:49:57}

 
**Benjamin Bengfort:** Yeah, the whole image dipping thing was like a good idea.
**Lawrence Gray:** at the time.
**Benjamin Bengfort:** It It's still a good idea. It just it needs more tuning. Like the RMSSE method of diffing
**Lawrence Gray:** Mhm.
**Benjamin Bengfort:** is not sufficient. Like I'm sure there there's another algorithm that would be better, but
**Lawrence Gray:** Yeah, maybe that should be one of the major things that if we decide to upgrade this to move toward.
**Benjamin Bengfort:** yeah, that' be great. Yeah, I mean I'm I'm just like spot checking a bunch of these images and they all look fine to me.
**Lawrence Gray:** Oh, okay.
**Benjamin Bengfort:** I know you can't see my screen. You're still looking at my VS Code.
**Lawrence Gray:** Yeah, I was wondering what you were talking about. So,
**Benjamin Bengfort:** Share what I'm looking at. So, I'm just like kind of going through, you know, like like this one. So, we went from the green line was going up to now the green line is going down. Like, whatever. Like, I don't know if I really care about that test-wise.
 
 

### 00:51:35 {#00:51:35}

 
**Benjamin Bengfort:** You know what I mean? Yeah. Look at this. We've just completely aborted. Green line goes up. Green goes down. But like you see these look basically the same, right? So it's fine. So yeah, this might be the random number generator thing you were talking about because like these are very different images, right? like you could see where a diff would just not
**Lawrence Gray:** Yeah.
**Benjamin Bengfort:** come up with a relationship. However, from an analytical perspective, you know, these sort of clusters one, two, and four in there like this is sort of a similar analytical result if that makes sense, you know, and so is this just because zero and two are in different positions. This is like the same like you this is what you would get from an ICDM, right? Both of these images would tell you the same thing, but like the diff would not match. So, I mean, this all looks fine to me. I mean, granted, I've only looked at like maybe 30 out of 311, but you know, at some point a little bit Okay, so that looks good.
 
 

### 00:54:34 {#00:54:34}

 
**Benjamin Bengfort:** Uh, we should upgrade Python, too. Here we're testing 38 39\. So we should test later versions of these, I think.
**Lawrence Gray:** Yeah.
**Benjamin Bengfort:** Um maybe do like 311 312\.
**Lawrence Gray:** 311.3 something like that. Yeah. I I typically work with 311 for everything that I work on.
**Benjamin Bengfort:** Yeah, because the error is no matching distribution found for mapplotib 310.3. no module named NLTK. So those modules must have um pin versions pinned to later versions of Python. All right. So let me just do that real quick. So we want to do 3.11 and 3.12. Or should we do 3.12 and 3.13?
**Lawrence Gray:** I I think we should do 311\. Um I think it's just a solid like um version
**Benjamin Bengfort:** Okay. So, 311 312 So that means Change some of these classifiers times.
**Lawrence Gray:** f\*\*\*.
**Benjamin Bengfort:** All right. So, I just changed a whole bunch of stuff. That should be fun. All right. Okay. So that so now I have everything doing 311 312 testing.
 
 

### 00:58:12 {#00:58:12}

 
**Benjamin Bengfort:** I've changed the Python version. So the minimum version that you can pip install Yellow Brick now with is going to be 3.10 10
**Lawrence Gray:** Okay. Can you
**Benjamin Bengfort:** uh
**Lawrence Gray:** can you switch screens? Yeah.
**Benjamin Bengfort:** to
**Lawrence Gray:** Uh, you're showing GitHub right now.
**Benjamin Bengfort:** um so what I did here in CI.yaml YAML I changed our matrix to run 3.11 and 3.12 tests
**Lawrence Gray:** Okay.
**Benjamin Bengfort:** on Abuntu Mac and Windows and then for Anaconda 311 312 and then 3.12 for doing the build.
**Lawrence Gray:** Okay.
**Benjamin Bengfort:** Um and then in setup.py pi here. Python requires greater than equal to 310 less than four
**Lawrence Gray:** Okay.
**Benjamin Bengfort:** where Python is have to change the build setup on this too now. It's fine. So um because I changed the CI I'll have to change like in GitHub like which checks are required to pass
**Lawrence Gray:** Mhm.
**Benjamin Bengfort:** because like if it requires Python 3.9 to pass and we're not running a Python 3.9 check then obviously that's dumb. All right.
 
 

### 01:00:53 {#01:00:53}

 
**Benjamin Bengfort:** The linting failed. That's fine. kind of failed because it couldn't find pi test spec which is less than ideal. Uh, but all of the other Python tests are running. So, I'm not sure why Anaconda is not working. But yeah, I mean, at this point, it's about just like chasing all this stuff down and fixing it.
**Lawrence Gray:** Okay.
**Benjamin Bengfort:** So,
**Lawrence Gray:** Um, you're working in a branch, right?
**Benjamin Bengfort:** I am.
**Lawrence Gray:** You can you can push push that branch and I can just work from it and I can fix the the remaining errors.
**Benjamin Bengfort:** Um I did.
**Lawrence Gray:** Okay.
**Benjamin Bengfort:** Um, yeah, I'm just looking at some of the exceptions that are happening. So, reax pattern didn't match, which means an error name probably changed. So, that'll be an easy fix. Um, there's an assertion error, which I think will be another easy fix because you just got to change it to what the actual value is. Um, artist lists object has no attribute remove.
**Lawrence Gray:** Yeah, I came across that one before.
 
 

### 01:02:54 {#01:02:54}

 
**Benjamin Bengfort:** So that's going to be a tricky one.
**Lawrence Gray:** Uh,
**Benjamin Bengfort:** Uh,
**Lawrence Gray:** it's it was a child actually. They they moved the remove method to some to a different place. Uh
**Benjamin Bengfort:** yeah, but you're going to have to do something like if has adder remove else. You know what I mean?
**Lawrence Gray:** yeah, I
**Benjamin Bengfort:** Otherwise, it won't be backwards compatible, which is super annoying.
**Lawrence Gray:** Yeah, I think I the way I What? How did I
**Benjamin Bengfort:** So, like for stuff like that, you have to make a decision, right?
**Lawrence Gray:** Yeah,
**Benjamin Bengfort:** So,
**Lawrence Gray:** that's more or less what I was kind of I was running into issues like that and not knowing what way to to say we're not going to worry about backwards compatibility. We're just going to we're just going to do it this way. So
**Benjamin Bengfort:** So for me it's like if there's like if it like if it advances the minimum version required to like the absolute latest version then I'm like less excited about that
 
 

### 01:04:01 {#01:04:01}

 
**Lawrence Gray:** Mhm.
**Benjamin Bengfort:** right because then it's like okay well this is you know MLI has done this to us in the past too where they like add something and then they revert so If it's like but if it like happened you know in in like two versions ago or something then I'm like sure like let's just move up to that two versions ago thing is probably stable or if it's a version that's been around for like six months or more
**Lawrence Gray:** Yeah,
**Benjamin Bengfort:** then
**Lawrence Gray:** it's been that particular one has been well over a year.
**Benjamin Bengfort:** great. Yeah. So in that case just we'll just make our mapplot live minimum dependency whatever that version is. Um, if it's just one thing then like
**Lawrence Gray:** All
**Benjamin Bengfort:** I can deal with it but if it's multiple things in the same package then I might just upgrade the dependency.
**Lawrence Gray:** right.
**Benjamin Bengfort:** Um like in the ideal case we're upgrading yellow brick with such frequency that like our dependencies will also upgrade like continuously. So like you know if if we were doing this and we were adding features or something and we came across this error when we were doing this be like okay we'll just update to the next version of mapplot lib and then someone came to us and was like well you know we want to use yellow brick but we were dependent on this other version of map output lib we can say oh well then you need to
 
 

### 01:05:19 {#01:05:19}

 
**Benjamin Bengfort:** use yellowbreak version 1.x X or lower, right? So, like that's the ideal situation because then you would you really would care less about backwards compatibility. You would just keep your library progressing with everyone else. But in order to do that, you need to have an update frequency that's about as frequent as your dependencies update frequently.
**Lawrence Gray:** Mhm.
**Benjamin Bengfort:** And again, that's one of the reasons why you really want to not have a lot of dependencies in library code. And that's one of the reasons that this project was so hard is because of the map plot lib and scikitlearn dependencies and just keeping up with them.
**Lawrence Gray:** Um okay. Um
**Benjamin Bengfort:** But yeah, I'm not seeing anything terribly difficult here. Like I think maybe the minimum version of mapl lib we can bump the minimum version of numpy we could probably bump. Um, we're going to have to change the is classifier, is aggressor, and is outlier check. Uh, there's a couple of stupid bugs. Um, but honestly, those will fix a lot of things.
 
 

### 01:06:40 {#01:06:40}

 
**Benjamin Bengfort:** Erase
**Lawrence Gray:** There's only 4 43 of them, right?
**Benjamin Bengfort:** What's that?
**Lawrence Gray:** It's only 43, right? Or issues.
**Benjamin Bengfort:** It's only 43, but updating map plot lib and numpy alone will probably take care of 30 of them.
**Lawrence Gray:** Okay. So, and as you're saying, we just don't go up to the latest one. Just go up to the minimum one that kind of covers the cover the majority of them, right?
**Benjamin Bengfort:** Yeah, I mean just you can ping me on Slack if you're
**Lawrence Gray:** Okay.
**Benjamin Bengfort:** not sure and I'm happy to do it. But yeah, it's just I mean just use your best judgment. Like
**Lawrence Gray:** Okay.
**Benjamin Bengfort:** if you think that the version that we're going up to is stable and it's not going to change, it's been around for a while and that everyone's gonna be fine using that version, then go ahead and upgrade to that version.
**Lawrence Gray:** Okay.
**Benjamin Bengfort:** But if it's like, you know, for example, like jumping from like pandas one to pandas 2, that's like an, you know, you know, like it's like does our library want to support that or not?
 
 

### 01:07:40 {#01:07:40}

 
**Benjamin Bengfort:** But like, you know, it just depends on
**Lawrence Gray:** Okay.
**Benjamin Bengfort:** how you feel about that version, I guess. Um,
**Lawrence Gray:** Okay.
**Benjamin Bengfort:** but yeah, I remember one time we upgraded to the latest version of Napot Lib and like the next month they broke everything and that's why in our requirements.txt we have a not 3.0.0
**Lawrence Gray:** Yeah.
**Benjamin Bengfort:** but I can I can say for sure that removing the 2.0.2 dependency we can get rid of that two two map 2 is so old now like we can just say only 3.4 four or above or whatever.
**Lawrence Gray:** Okay.
**Benjamin Bengfort:** That's that's perfectly fine.
**Lawrence Gray:** All right. Cool. Well, I can Well, I can take it from here then.
**Benjamin Bengfort:** All right. Yeah, just ping me on Slack if uh you need anything
**Lawrence Gray:** Okay, we'll do.
**Benjamin Bengfort:** when I can.
**Lawrence Gray:** All right. Thanks, man. I appreciate it. You have a good night.
**Benjamin Bengfort:** Sure. Yeah. No, I appreciate you keeping this library up to date and I'm glad to hear everything's well.
 
 

### Transcription ended after 01:08:57

*This editable transcript was computer generated and might contain errors. People can also change the text after it was created.*
