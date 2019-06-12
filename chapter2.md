Li Suyin's phone didn't have an alarm app, she would have to program something up once she learned more about python. She found herself sleeping in fits and starts until it was time to get up, have breakfast and head to her first class.

Li Suyin knew she would have to get into cybernetic enhancements before long, but first she wanted to establish her bonafides in programming, to get a firm foundation which would help her move forward in algorithms, flow and enhancements.

Elder Hua Su taught the programming class. Li Suyin got there early, but even after the smaller classroom filled in, it was only about 30 people.

"New programmers on the left, those familiar with the basics on the right," Elder Su said.

Li Suyin moved over to the right side of the room.

A few more students trickled in over the next few minutes until at last, the matronly elder made a sharp gesture with her right hand and the door snapped shut.

“Consider this my first lesson. Lateness will not be tolerated,” she said crisply, sweeping the room with an intimidating stare. “If you are late, you will not receive my instruction that day. There will be no exceptions. Nor will I allow interruptions. Any purposeful disruption of my lesson will result in your immediate expulsion from this room. You will not be allowed back.”
The few whispers and sounds from the students presented ended immediately. The Elder regarded them silently for a beat. “Good. You can follow instructions,” she said with a small amount of satisfaction. 


“I am Elder Hua Su. I am the Head of our Programming department. You will refer to me as Elder Su, Programmer Su, or Instructor, and nothing else. You are here because you have had no instruction in programming for whatever reason.” There was no judgement in the Elder’s words, only a statement of fact. 

Li Suyin resented that statement, she wanted to learn more and especially get some early pointers for learning python.

“Or because you desire expert advice in setting your foundation. In that case, I applaud your humility. Everything you will learn here at the Sect is founded in your familiarity with programs and algorithms, which you will learn the beginning notes of here."

Expert advice, that sounded right to Li Suyin.

"I will not waste time on command lines and syntax errors, for it is the substance that you need to learn. If you do not strive and push past minor obstacles such as those, you will never make it in the sect. To avoid wasting time I will divide the classroom as I intended."

A shimmering glass pane mirror slid down from the ceiling dividing the class into two, and Li Suyin suspected it allowed two separate holograms of the Elder to be displayed in the two halves of the room.

"Good. Now after the very first steps of your programmer's art, progress is made more effective by self directed learning. I will teach you a few things, but most of our class time will be spent working on assignments where I will come alongside and offer one on one feedback. My focus is on your problem solving process. The Programmer's art, qua programming, is a slow art, taking time and conscious direction to solve the big problems. Your problem solving skills are much more important than your typing skills in this area.

"As a test, I'd like you to start with writing a python program which both pretty prints the current date and time, and also displays a number indicating the number of milliseconds since the emperor took the throne. You may be unfamiliar with python, so you can also use any other language available in our environment. However, I want you to actually calculate the milliseconds number from the parts of the current date and time, not rely on a language facility which directly looks at the linux time.

"I will offer points as you work through this."

Li Suyin was determined to figure it out in Python, especially since C# and F# didn't seem to be available. Father had spoken of Ocaml, a pre-cursor language to F#. Maybe that was available, but she wasn't familiar with the libraries of Ocaml, so she went with python instead.

The first part was finding out what sort of datetime library python had:

    Source code: Lib/datetime.py The datetime module supplies classes for manipulating dates and times in both simple and complex ways. While date and time arithmetic is supported, the focus of the implementation is on efficient attribute extraction for output formatting and manipulation. For related functionality, see also the time and calendar modules.

classmethod datetime.today()

    Return the current local datetime, with tzinfo None. This is equivalent to datetime.fromtimestamp(time.time()). See also now(), fromtimestamp().
    The Sect didn't provide access to the empire's internet, but it did replace the normal Multitudes searchmasters' sect with a local search of sect resources available to her. So her normal search query (multitude -luckymode "python datetime") was redirected to sect-hunt -topn 1 "python datetime"

She started coding up the simple part of the test: displaying the current datetime in a readable format:


    [pytest1.py] 

    from datetime import datetime

    print (datetime.today()) 


Pretty easy once the docs are available.

    $ python pytest1.py 

    43-01-1 20:25:41.372618

Now the hard part. There's some off by one issues since year 1 is the first one (add 0 years), week 1 is the first one, day 1 is the first one. etc.

01-01-1 01:01:01.000001 would be the first moment of the current emperor's reign, so Li Suyin thought by subtracting by one from them all, she could get the correct offsets, and then divide micros by 1000 to get millis.



Instance attributes (read-only):

    datetime.emperor

    String value of the reigning emperor/empress of the current date 

    datetime.year
    Between 1 and 1000 inclusive. 

    datetime.week
    Between 1 and 52 inclusive. s:

    datetime.day
    Between 1 and 7 inclusive.

    datetime.hour
    In range(24). 

    datetime.minute
    In range(60). 

    datetime.second
    In range(60). 

    datetime.microsecond
    In range(1000000).


     $ vim pytest1.py

    :saveas su_test1.py

    [su_test1.py]
    from datetime import datetime 

    dt = datetime.today()
    print(datetime.today())
    year = dt.year - 1
    week = dt.week - 1
    day = dt.day - 1
    hour = dt.hour - 1
    minute = dt.minute - 1
    second = dt.second - 1
    milliseconds = (dt.microsecond - 1) / 1000
    week = week + year * 52
    day = day + week * 7
    hour = hour + day * 24
    minute = minute + hour * 60
    second = second + minute * 60
    milliseconds = milliseconds + second * 1000
    print(milliseconds) 

    $ python3 su_test1.py

    43-01-1 20:25:41.372618
    1320953080372.618


 Li Suyin raised her hand, passing her phone to the Elder after she had checked a few other disciple's results.

"Another correct result. You may want to consider creating an offset helping function, and in a larger program you'd want to model unit conversions explicitly, but in a quick classroom setting it's good."

Other disciples rapidly finished the assignment, a few of them weren't done yet after 20 minutes, 40% had forgot the off-by-one issue, and had to fix their code, and 50% had correct results.

"Those of you who can't figure out the basics of this test, keep working on it. The rest of you, let's commence the instructional portion of this class."

Elder Su's "instructional" material was largely preparatory. She spoke on the need for slow, deliberate thinking, required all students to come to class with paper, and extolled the benefits of thinking on paper, make some funny comments and comparisons with Elder Qiu's flow classes, and began expounding on a first challenge problem involving sect rankings.

She also offered up an extended version of the datetime problem: "The emperors class in the datetime module contains the years of each emperor's reign. You can access all the emperors and their corresponding reign duration as a dict. Using this feature, and considering year 1 in your system to be the start of the Empress' reign, calculate the milliseconds from year 1 of the Empress' reign to 22-50-1 00:00:00 of Emperor's An's reign. This will be a negative number."

Li Suyin had hoped they would get something better than these phones in class, but it wasn't to be, so she went back to the house after class, had lunch, and spent some time investigating cybernetics.


CYBERNETIC ENHANCEMENT ASSESSMENT: Li Suyin

INSTALLED: None

Status:

BRAIN
-- Conscious - unqualified
(suitedness requirement met, preconditions: heart / lungs not met)
-- Subconscious - unqualified
-- Autonomic - unqualified

Lungs : unqualified
Heart : unqualified
Legs : unqualified
Hands : unqualified
Arms : unqualified
Spine : unqualified
Eyes : unqualified
Face : unqualified
Other : unknown


HELP ENHANCEMENTS

Argent Sect Enhancements:

Micro, Minor and Modest enhancements are general enhancers provided by the sect. Significant, substantial, large enhancements are specialized for specific effect and available for advanced disciples based on progression in sect challenges and opportunities.

Brain enhancements require blood flow improvement from the lungs and heart, guaranteeing an amplified brain will have the fuel it needs.

Micro - 2 argent coins
Minor - 10 argent coins
Modest - 25 argent coins


HELP QUALIFICATIONS

As every part of the body and brain is inter-related, greatly improving one part of the body has an impact on the connected parts. By strengthening the body first, the shock to the system caused by cybernetics will be lessened.

There are training exercises for every part of the body to help you reach the qualification standard for safe cybernetic enhancements.

In addition there are dependent conditions for development, because of the inter-related nature of the body and mind (+1 means one level higher in tier of enhancement).

HEART <= LUNGS + 1
LEGS <= HEART + 1
HANDS <= ARMS + 1
ARMS <= HEART + 1
ARMS <= SPINE + 1
EYES <= FACE + 1
FACE <= HEART + 1

Autonomic <= SPINE + 1
Autonomic <= HEART
Subconscious <= HEART
Conscious <= HEART

There are additional specialized parts of the body and mind that can be enhanced as an advanced cyberneticist.


Li Suyin didn't see Su Ling all day, though she was in the computer room all afternoon completing Elder Su's two challenges and making up some additional ones of her own.

She went to the dispensary to eat something quick (and hacker-friendly), unwind and get ready for Elder Qui's class. 
