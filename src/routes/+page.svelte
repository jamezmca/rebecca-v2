<script>
    import ContactForm from "../components/ContactForm.svelte";

    let headerHeight;
    let y;
    let displayFAQ = [];
    let showTestimonial = 0;
    let showMenu = false;

    let navLinks = ["about", "services", "FAQ", "contact"];
    const keyWords = [
        "Anxiety",
        "Eating disorders",
        "Relationship difficulties",
        "Body image",
        "Trauma & PSTD",
        "Disordered eating",
        "OCD",
        // "Exercise addiction",
        // "Sexuality",
        "Loss & grief",
        "Life transitions",
        "Depression",
        "Conflict",
        "Attachment issues",
        "Self-esteem & self-criticism",
        "Personal growth ",
    ];

    const services = [
        {
            name: "consultation",
            content: "Book a free 15 minute phone consultation",
            link: "https://beckybradleycounselling.janeapp.com",
        },
        {
            name: "counselling",
            content: "50 minute individual counselling session",
            link: "https://beckybradleycounselling.janeapp.com",
        },
        {
            name: "location",
            content: "Sessions available online only",
            link: "#FAQ",
        },
    ];

    let testimonials = [
        `Working with Becky has helped me make tough decisions and become stronger in my self-awareness.  When I first started working with Becky, I was in the midst of huge changes in my life, transitioning to ending a long-term relationship and moving out on my own for the first time. I don't know how I would have handled all these big changes without her support and empathy. Throughout our time together, I can honestly say that I know myself so much better and am able to make tough decisions, put my needs first, and take care of myself. I also appreciate her flexibility and willingness to work with me on whatever I come into the session with. Whether I come in to talk about relationship issues or my eating disorder, either way, Becky is non-judgmental, empathetic, compassionate, and actively listens. I always leave our sessions feeling better than when we started. I feel heard and genuinely cared for. I have learned to be more assertive, outgoing, confident, self-aware, and ambitious from working with Becky. Currently, I am in another big transition, and I feel way less anxious and more confident navigating through it knowing that I am going to discuss it with Becky. I can’t thank her enough for how much growth I have had in my life since our work started together early in 2022. Now, I am looking forward to seeing what my future holds and confident that I will make the best of it.`,
        `It is an absolute pleasure to work with Becky. I always feel so supported, heard and seen. Her approach is warm and kind and I feel safe to be my full self with her. I have found the work we have done together to be extremely helpful. Now seeing the anxiety and fear in a completely different light, I am able to offer a lot more compassion towards myself. I highly recommend working with Becky, she's wonderful!`,
        `I've been working with Becky for a few months now. At the start of the year I found myself needing help with a few mental health issues, so of course I reached out to a few therapists and Becky contacted me the very next day (a Saturday) (and Becky was the only one to make contact), the personal phone call from Becky told me that this therapist was caring and loved what she did. We made a connection instantly. I felt comfortable with Becky from that first phone conversation. Our first few sessions were focused more on us getting to know each other and talking about my issues I wanted to tackle, again, I felt so comfortable and connected to Becky. We then started getting into what I needed. It takes a lot to talk openly about your life, issues, etc but with Becky I felt confident and relaxed which made the process so much easier. And believe me it was & is a process, but with Becky I trusted the process and journey we were embarking on and I've never looked back. I don't like to think where I'd be without Becky, the tools and care Becky has and is sharing with me to help me through my process is beyond outstanding, I am such a better person for my time with Becky, my marriage is stronger, I am a happier, healthier person, a more understanding person, I finally love myself for all that I am, and honestly, I couldn't have asked for better. Loving yourself is actually quite difficult, but thanks to Becky I do, which helps me better a person. I was a person that suppressed everything (for decades) it wasn't a healthy relationship I had with myself, which in turn I didn't have great relationships with others, by my word, working, trusting and having the right tools I am definitely on a better path than I was. I am still on this journey to healing and self love but I know I am with the right person. Becky is in this for the love of what she does, and it seriously shows through our time together. Thank you Becky, I appreciate you more than you will every realize.`,
        `Becky is great at creating a comfortable and safe space to discuss any mental health issues and life challenges. Her skill in posing the right questions, allows me space to reflect and re-evaluate the ways I see and respond to situations. I’m learning a lot about myself and seeing benefits in my overall mental health and wellbeing. I find as a result that my relationships with others are more fulfilling and reciprocal.`,
        `I had such an awesome experience having Becky as my therapist when I was going through an interesting transitional period in my relationship leading up to my wedding. From the first session, I felt heard, validated and definitely felt she would be a good fit for me. She helped me figure out what I wanted out of therapy and we achieved it in a way where I didn't feel anxious parting ways with her. I was able to come away from therapy with the tools necessary for me to function well and independently regardless of what I might go through in the future. When I started sessions with Becky I didn't exactly know how to deal with past trauma (that I didn't even realise I had or was affecting me) and now I feel I am a confident adult with a broader understanding of myself, how I react to things and situations, why I deal with them a certain way and how I can best work through them and move on through life. My anxiety is minimal now and I have Becky to thank for that. I love knowing that even though I've finished my sessions with her I can schedule a meeting with her if I ever feel I need to talk to someone and can see myself utilising that options when I begin transitioning into the next phase of my life if needed. In terms of connecting with her, I found her website and booking platform super easy and most of the time Becky would just pre book during our sessions and I would get simple emails and calendar events all automated so it was super seamless for me. I found her super flexible with any sessions I needed to chnge or move around and it made my life a lot easier admin wise. I highly recommend therapy in general but definitely as a therapist, I couldn't recommend Becky enough!`,
        `I have had an incredibly positive experience with Becky. Becky consistently creates a safe and comfortable environment for me in counselling. She uses evidence based approaches while always being non-judgmental, compassionate, supportive and authentic. Her work and guidance has helped me navigate through my own mental health concerns, through tough situations, and uncertain times. Working with Becky unlocks moments of life changing self discovery for me. Becky understands that counselling looks different for everyone and is willing to find what respectively works for you. I genuinely highly recommend Becky to anyone seeking help or support with any topic.`,
    ];

    const faq = [
        {
            question:
                "What are your counselling qualifications and experience?",
            answer: "I have an Undergraduate degree (BA) in Human Geography and Psychology from the University of British Columbia in Vancouver, Canada and a Master’s degree in Counselling Psychology from Adler University in Vancouver, Canada. Prior to starting my private practice, I worked as a counsellor with the Looking Glass Foundation for Eating Disorders in Vancouver, Canada. I am committed to ongoing professional and personal development as a therapist. A few of my additional qualifications/trainings include: Introduction & Deepening - Internal Family Systems (Mind Beyond Institute), Internal Family Systems for Complex Trauma (PESI), CBT-E - Enhanced Cognitive Behavior Therapy (Centre for Research on Eating Disorders at Oxford), Temperament Based Therapy with Support for Anorexia Nervosa (TBT-S Institute), LivingWorks – safeTALK & Skillfully Responding to Distress – (The Crisis Intervention and Suicide Prevention Centre of British Columbia) and Trauma-Informed Practice – Level 1 Certificate.",
        },
        {
            question: "Are you a Registered Counsellor in New Zealand?",
            answer: "Yes, I am a Registered Counsellor with the New Zealand Association of Counsellors.",
        },
        {
            question:
                "It is my first time coming to counselling, what if I am nervous and don’t know what to talk about?",
            answer: "It is completely normal and very common to feel nervous about a first counselling session. I like to remind my clients that they are in the driver seat, and as a counsellor, I am in the passenger seat, meaning that there are no obligations, and I will go at your own pace. As a counsellor, it is my role to ask the right questions, even if you're uncertain about what specifically is bothering you. During a first counselling session, we will review informed consent and I will ask a variety of questions that will provide some guidance. Any questions you may have can be answered at this time, or at any point throughout counselling. Building a strong therapeutic relationship is vital for successful therapy, and I understand that different clients have different preferences. Some clients prefer uninterrupted self-expression, while others appreciate more structure or guidance. Your session will be tailored to your preferences and what makes you comfortable. Ultimately, in the first session, I want to help you feel as comfortable as possible and get to know you better!",
        },
        {
            question: "What can I expect from the consultation call?",
            answer: "Before meeting for a full session of counselling, I offer a consultation call for us to get to know each other a bit better. The consultation call gives you an opportunity for you to ask any questions you might have, discuss your counselling goals and determine whether we are a good fit. (Numerous academic studies on effective counselling consistently highlight the importance of the client-therapist relationship as a major factor in achieving success.) During our conversation, I'll share my counselling approach and give you a clear picture of what you can expect if you choose to work with me. Additionally, I will inquire about what has brought you to counselling and what you hope to get out of coming to therapy.",
        },
        {
            question: "What can I gain from counselling?",
            answer: "Speaking freely in a safe and truly non-judgemental atmosphere is designed to be therapeutic, and can enable you to face and embrace your truths. While confiding in a friend or family member can be valuable, meeting with a qualified therapist provides distinct advantages. Therapists offer diverse perspectives and an array of tools to help tackle your specific challenges. Therapists aim to be both non-judgmental and empathetic in their listening and help clients understand how their experiences may be driving certain behaviours, thoughts or feelings. As you work with the right counsellor, you'll gradually develop comfort and confidence in the process. This growth allows for deeper exploration of emotions, leading to clarity in identifying and addressing problems. Many individuals report an array of valuable outcomes from the counselling process, a few include: healthier relationships with self and others, increased self-awareness, self-esteem and the adoption of positive coping strategies.",
        },
        {
            question: "What is your approach to therapy?",
            answer: "My approach is rooted in a variety of evidence-based modalities, including attachment-based therapy, emotion-focused therapy, internal family systems, person-centered therapy and trauma-informed care. I tailor my therapy approach to each client based on their unique needs, experiences and goals.  I actively encourage clients to voice their questions, concerns and provide feedback throughout the therapeutic process in order to meet their goals and needs. Part of my job is to help clients develop a deeper understanding of themselves, their relationships, and their experiences, and to provide them with the tools and strategies they need to achieve their goals and live more fulfilling lives.",
        },
        {
            question: "How much does a counselling session cost?",
            answer: "$165.00 NZD (GST INCL.) for a 50 minute counselling session.",
        },
        {
            question: "Do you offer sliding scale therapy?",
            answer: "I offer a limited number of sliding scale rates for those facing financial barriers in accessing therapy. At this time, all of my sliding scale rates are currently full.",
        },
        {
            question: "Do you provide in-person counselling?",
            answer: "I am currently only offering online counselling which takes place via a secure encrypted video calling platform.",
        },
        {
            question: "What is your cancellation policy?",
            answer: "I have a 24hr cancellation policy, meaning that any session can be cancelled or re-scheduled up to 24hrs before the time of the appointment. If less than 24hrs notice of a cancellation is provided, or in the case of a no show, the cost of the session will be charged in full. Considerations may be made in the case of an emergency and will be discussed on a case-by-case basis.",
        },
        // {
        //     question: "What can I expect from a counselling session?",
        //     answer: "In a counselling session you can expect a comfortable and pressure-free space to discuss the concerns weighing on you. As a counsellor, it is my role to ask the right questions, even if you're uncertain about what specifically is bothering you. In our initial session, we will review the informed consent form together, which outlines my counselling background, confidentiality and what counselling entails. The sessions are collaborative, allowing me to tailor my therapeutic approach to your unique needs. Building a strong therapeutic relationship is vital for successful therapy, and I understand that different clients have different preferences. Some clients prefer uninterrupted self-expression, while others appreciate more structure or guidance. Your session will be tailored to your preferences and what makes you comfortable.",
        // },
        {
            question: "How many sessions does counselling take?",
            answer: "The number of counselling sessions varies for each individual and situation, as there is no set formula. We will collaboratively consider your unique circumstances when determining the frequency and duration of sessions. While acute issues or crises may require regular sessions for a shorter period, many clients transition to less frequent appointments, to sustain their mental health and well-being. This journey is highly personalised, and together we will discuss a plan based on your goals, needs, and available resources.",
        },
        // {
        //     question: "I have other questions for you, how can I reach you?",
        //     answer: "If you have any further questions about anything at all, please contact me via my email at beckybradleycounselling@gmail.com, the contact form below, or book a free consultation call.",
        // },
        {
            question: "I’ve decided to come to therapy, now what?",
            answer: "You can email me at beckybradleycounselling@gmail.com, send me a message with the contact form below or use the Book Now button to schedule a consultation session. I look forward to hearing from you!",
        },
    ];

    const favorites = [
        "Eating disorders",
        "Anxiety",
        "Relationship difficulties",
    ];
</script>

<header
    bind:clientHeight={headerHeight}
    class={"duration-200 sticky top-0 relative border-b border-solid z-20   " +
        (y > 0 ? "bg-white border-indigo-400 shadow" : " border-transparent")}
>
    <div
        class={"max-w-[1200px] mx-auto w-full flex items-center justify-between gap-4 duration-200 px-6 sm:px-8 " +
            (y > 0 ? " py-4 sm:py-6 " : " py-6 sm:py-8  ")}
    >
        <!-- <h2
            class="hidden sm:inline font-medium text-left text-2xl sm:text-3xl md:text-4xl font-semibold"
        >
            Becky Bradley Counselling
        </h2> -->
        <a
            href="/"
            class="flex text-center flex-row gap-1 font-medium sm:text-lg"
        >
            <h2>Becky Bradley</h2>
            <h2 class="">Counselling</h2>
        </a>
        <nav
            class="hidden sm:text-sm lg:text-base md:flex items-center gap-2 sm:gap-4 md:gap-5"
        >
            {#each navLinks as navLink}
                <a
                    href={`#${navLink}`}
                    class="capitalize relative cursor-pointer overflow-hidden group"
                >
                    <p>{navLink}</p>
                    <div
                        class="absolute bottom-0 right-full group-hover:translate-x-full duration-300 h-[1.5px] w-full bg-slate-800"
                    />
                </a>
            {/each}
            <a
                href="https://beckybradleycounselling.janeapp.com"
                target="_blank"
                class="bg-indigo-400 text-white text-lg px-4 py-2 rounded-lg hover:bg-indigo-300 duration-200 border-2 border-solid border-indigo-200"
                >Book now</a
            >
        </nav>
        <button
            on:click={() => (showMenu = !showMenu)}
            class={"px-1 aspect-square text-xl rounded grid place-items-center cursor-pointer duration-200  md:hidden "}
        >
            <i class="fa-solid fa-bars" />
        </button>
    </div>
    {#if showMenu}
        <div
            class="absolute top-0 left-0 w-full px-4 pb-4 flex flex-col gap-4 bg-white shadow"
        >
            <div
                class="flex items-center justify-between gap-4 border-b-[1.5px] border-solid border-indigo-400 py-4"
            >
                <h2>Menu</h2>
                <i
                    on:keydown={() => {}}
                    on:click={() => (showMenu = !showMenu)}
                    class="fa-solid fa-xmark text-lg cursor-pointer hover:opacity-60 duration-200"
                />
            </div>
            {#each navLinks as navLink}
                <div on:click={() => (showMenu = false)}>
                    <a href={`#${navLink}`} class="text-sm capitalize"
                        >{navLink}</a
                    >
                </div>
            {/each}
            <a
                href="https://beckybradleycounselling.janeapp.com"
                target="_blank"
                class="bg-indigo-400 text-white text-lg sm:text-xl md:text-2xl font-medium border-2 border-solid border-indigo-200 rounded-lg px-4 py-2 hover:bg-indigo-300 duration-200 text-center"
                >Book now
            </a>
        </div>
    {/if}
</header>

<main class="flex flex-col gap-10 text-sm sm:text-base">
    <section
        style="min-height: calc(100vh - {headerHeight}px)"
        class="flex flex-1 flex-col items-center justify-center md:flex-row gap-4 md:gap-10 lg:gap-14 px-6 sm:px-8 max-w-[1200px] mx-auto w-full"
    >
        <div
            class="flex flex-col md:flex-1 justify-center items-center gap-4 sm:gap-6 md:gap-8 text-center md:text-left"
        >
            <h1 class="text-4xl sm:text-5xl md:text-6xl font-semibold">
                Take a step towards
                <b class="text-indigo-400">healing</b> and
                <b class="text-indigo-400">growth</b>
            </h1>
            <p class="text-sm sm:text-base">
                Step into a space of <b class="font-normal text-indigo-500"
                    >non-judgement, trust and empowerment</b
                >, where together we will discover your path to healing. As your
                therapist, I will assist you in recognising and developing your
                inherent strengths, knowledge and self-awareness to
                <b class="font-normal text-indigo-500">overcome challenges</b>
                and
                <b class="font-normal text-indigo-500">achieve your goals</b>.
            </p>
            <a
                href="https://beckybradleycounselling.janeapp.com"
                target="_blank"
                class="bg-indigo-400 text-white text-lg sm:text-xl md:text-2xl font-medium border-2 border-solid border-indigo-200 rounded-lg px-4 py-2 mx-auto md:mr-auto md:ml-0 hover:bg-indigo-300 duration-200"
                >Book now
            </a>
        </div>
        <div
            class="flex max-w-[60vw] sm:max-w-[50vw] md:max-w-[40vw] mx-auto w-full flex-col md:flex-1 lg:justify-center lg:items-center"
        >
            <img
                src="/profile3.jpeg"
                alt="profile-img"
                class="rounded-full object-cover aspect-square shadow-xl"
            />
        </div>
    </section>
    <section
        id="about"
        class="flex flex-col gap-8 sm:gap-10 md:gap-14 pb-12 sm:pb-16 md:pb-20 px-6 sm:px-8 max-w-[1200px] mx-auto w-full"
    >
        <p class="font-semibold text-lg sm:text-xl md:text-3xl mx-auto">
            A bit about me
        </p>
        <h1
            class="text-4xl sm:text-5xl md:text-6xl -mt-4 font-semibold max-w-[700px] mx-auto w-full text-center"
        >
            Experienced in <b class="text-indigo-400">helping</b> you feel your
            <b class="text-indigo-400">best</b>
        </h1>
        <div
            class="flex flex-col gap-4 text-sm sm:text-base max-w-[700px] mx-auto w-full text-center sm:text-justify"
        >
            <p class="">
                I am a Registered Counsellor with the New Zealand Association of
                Counsellors based in Aotearoa (New Zealand), who is passionate
                about helping individuals with their mental health. I hold a
                Master’s degree in Counselling Psychology and specialise in
                anxiety, eating disorders and relationship difficulties. Having
                had the privilege of growing up in six countries, I have a deep
                appreciation for diverse identities, cultures and backgrounds.
            </p>
            <p class="">
                When I'm not outdoors, running, playing board games or enjoying
                time with loved ones, I'm dedicated to making quality therapy
                accessible to all. Through my personal journey, I've witnessed
                firsthand the incredible impact therapy can have. Join me on
                this empowering path towards change. I provide individual
                counselling for a variety of needs including:
            </p>
        </div>
        <div
            class="flex items-center flex-wrap gap-2 sm:gap-4 max-w-[700px] mx-auto w-full justify-center"
        >
            {#each [...keyWords].sort() as keyWord}
                <div
                    class={" py-2 rounded text-xs sm:text-base px-3 z-10 relative flex items-center justify-center gap-2 text-white relative sm:flex-1 text-center " +
                        (favorites.includes(keyWord)
                            ? " bg-indigo-600"
                            : ["bg-indigo-400", "bg-indigo-400"][
                                  Math.floor(Math.random() * 2)
                              ])}
                >
                    {#if favorites.includes(keyWord)}
                        <i class="fa-solid fa-star" />
                    {/if}
                    <p class="whitespace-nowrap">{keyWord}</p>
                </div>
            {/each}
        </div>
        <a
            href="#FAQ"
            class=" px-4 py-2 rounded-lg bg-white border-[1.5px] border-solid duration-200 cursor-pointer hover:border-indigo-200 mx-auto border-indigo-400 text-indigo-500 text-sm -my-4"
            >Learn more</a
        >
    </section>
    <section
        id="services"
        class="flex flex-col gap-8 sm:gap-10 md:gap-14 py-14 sm:py-20 text-white bg-indigo-400 px-6 sm:px-8"
    >
        <p class="font-semibold text-lg sm:text-xl md:text-3xl mx-auto">
            Services I offer
        </p>
        <h1
            class="text-4xl sm:text-5xl md:text-6xl -mt-4 font-semibold max-w-[700px] mx-auto w-full text-center"
        >
            Feeling stuck? I'm here to help!
        </h1>
        <p
            class="text-sm sm:text-base max-w-[700px] mx-auto w-full text-center"
        >
            I will work collaboratively with you to achieve your goals using
            tailored therapeutic approaches and techniques. I use a
            compassionate and empathetic approach to create a safe and
            supportive space where you can explore your emotions, thoughts and
            behaviours.
        </p>
        <div
            class="flex flex-col sm:flex-row gap-4 sm:gap-6 max-w-[1000px] mx-auto w-full"
        >
            {#each services as service}
                <a
                    href={service.link}
                    target={service.name !== "location" ? "_blank" : ""}
                    class="p-2 sm:p-4 cursor-pointer flex-1 text-slate-800 rounded-lg bg-white specialShadow flex flex-col gap-2 sm:gap-4"
                >
                    <div
                        class="flex items-center text-indigo-600 justify-between gap-4 text-lg sm:text-xl md:text-2xl font-semibold capitalize"
                    >
                        <h3 class="">{service.name}</h3>
                        {#if service.name === "consultation"}
                            <i class="fa-solid fa-phone" />
                        {:else if service.name === "counselling"}
                            <i class="fa-solid fa-comments" />
                        {:else if service.name === "location"}
                            <i class="fa-solid fa-earth-americas" />
                        {/if}
                    </div>
                    <div class="flex items-center flex-1 justify-center">
                        <p class="text-center">{service.content}</p>
                    </div>
                </a>
            {/each}
        </div>
    </section>
    <section
        id="FAQ"
        class="flex flex-col gap-8 sm:gap-10 md:gap-14 py-6 sm:py-10 md:py-14 px-6 sm:px-8 max-w-[1200px] mx-auto w-full"
    >
        <h1
            class="text-4xl sm:text-5xl md:text-6xl font-semibold max-w-[700px] mx-auto w-full text-center"
        >
            FAQ
        </h1>
        <p
            class="text-sm sm:text-base max-w-[700px] mx-auto w-full text-center"
        >
            <b>Please note </b> that I am unable to provide crisis or emergency support.
            If you require urgent care, please contact your local emergency service
            or crisis line.
        </p>
        <div
            class="flex flex-col gap-4 select-none max-w-[800px] mx-auto w-full"
        >
            {#each faq as question, questionIndex}
                <button
                    on:click={() => {
                        if (displayFAQ.includes(questionIndex)) {
                            displayFAQ = displayFAQ.filter(
                                (val, valIndex) => val !== questionIndex,
                            );
                            return;
                        }
                        displayFAQ = [...displayFAQ, questionIndex];
                    }}
                    class="flex flex-col gap-4 sm:gap-6 p-4 border-l-[1.5px] duration-200 cursor-pointer group border-solid border-indigo-400"
                >
                    <h4
                        class="group-hover:pl-2 duration-200 sm:text-lg text-left"
                    >
                        {question.question}
                    </h4>
                    {#if displayFAQ.includes(questionIndex)}
                        <p
                            class="text-slate-600 pl-2 text-sm sm:text-base text-left"
                        >
                            {question.answer}
                        </p>
                    {/if}
                </button>
            {/each}
        </div>
    </section>
    <section
        id="testimonials"
        class="flex flex-col gap-8 sm:gap-10 md:gap-14 py-14 sm:py-20 bg-white px-6 sm:px-8 -mb-10"
    >
        <p
            class="text-4xl sm:text-5xl md:text-6xl text-indigo-400 font-semibold text max-w-[700px] mx-auto w-full text-center"
        >
            See what people are saying!
        </p>
        <div class="flex flex-col gap-4 sm:gap-8">
            <p
                class="text-slate-600 italic max-w-[1200px] w-full mx-auto font-light text-justify"
            >
                {testimonials[showTestimonial]}
            </p>
            <div class="flex items-center mx-auto gap-2">
                {#each testimonials as item, itemIndex}
                    <button
                        on:click={() => (showTestimonial = itemIndex)}
                        class={"w-3 sm:w-3.5 rounded-full aspect-square border border-2 border-indigo-400  duration-200 " +
                            (itemIndex === showTestimonial
                                ? "bg-indigo-400"
                                : "hover:bg-indigo-400")}
                    >
                    </button>
                {/each}
            </div>
        </div>
    </section>
    <section
        id="contact"
        class="flex flex-col gap-8 sm:gap-10 md:gap-14 py-14 sm:py-20 text-white bg-indigo-400 px-6 sm:px-8"
    >
        <h1
            class="text-4xl sm:text-5xl md:text-6xl font-semibold max-w-[700px] mx-auto w-full text-center"
        >
            Contact me
        </h1>
        <p
            class="text-sm sm:text-base max-w-[700px] mx-auto w-full text-center"
        >
            For any questions, qualms or queries you may have!
        </p>
        <!-- <i class="fa-solid fa-envelopes-bulk mx-auto text-2xl" /> -->

        <ContactForm />
        <div class="flex items-center mx-auto">
            <p>Or get in touch at beckybradleycounselling@gmail.com</p>
        </div>
    </section>
</main>

<footer
    class="py-20 px-8 flex items-center justify-center text-sm sm:text-base"
>
    <div class="mx-auto max-w-[600px] w-full flex flex-col gap-4 text-center">
        <p>Copyright © 2023 Becky Bradley Counselling</p>
        <a
            class="text-indigo-400"
            href="https://www.smoljames.com"
            target="_blank">Website by James Development</a
        >
    </div>
</footer>

<svelte:window bind:scrollY={y} />
