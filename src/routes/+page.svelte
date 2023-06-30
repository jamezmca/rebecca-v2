<script>
    import ContactForm from "../components/ContactForm.svelte";

    let headerHeight;
    let y;
    let displayFAQ = [];
    let showMenu = false;

    let navLinks = ["about", "services", "FAQ", "contact"];
    const keyWords = [
        "Anxiety",
        "Eating disorders",
        "Relationship difficulties",
        "Body image",
        "Trauma & PSTD",
        "Disordered eating",
        "Exercise addiction",
        // "Sexuality",
        "Loss & grief",
        "Life transitions",
        "Depression",
        "Self-esteem & self-criticism",
        "Conflict",
        "Attachment issues",
        "Compulsivity & addiction",
    ];

    const services = [
        {
            name: "consultation",
            content: "Book a free 15 minute phone consultation",
        },
        {
            name: "counselling",
            content: "50 or 75 minute individual counselling session",
        },
        { name: "location", content: "Sessions available online only" },
    ];

    const faq = [
        {
            question:
                "What are your counselling qualifications and experience?",
            answer: "I have an Undergraduate degree (BA) in Human Geography and Psychology from the University of British Columbia in Vancouver, Canada and a Master’s degree (MCP) in Counselling Psychology from Adler University in Vancouver, Canada. Prior to starting my private practice, I worked as a counsellor with the Looking Glass Foundation for Eating Disorders in Vancouver, Canada. I am committed to ongoing professional and personal development as a therapist. A few of my additional qualifications/trainings include: Introduction & Deepening - Internal Family Systems (Mind Beyond Institute), Internal Family Systems for Complex Trauma (PESI), Temperament Based Therapy with Support for Anorexia Nervosa (TBT-S Institute), LivingWorks – safeTALK & Skillfully Responding to Distress – (The Crisis Intervention and Suicide Prevention Centre of British Columbia) and Trauma-Informed Practice – Level 1 Certificate.",
        },
        {
            question:
                "It is my first time coming to counselling, what if I am nervous and don’t know what to talk about?",
            answer: "It is completely normal and very common to feel nervous about a first counselling session. I like to remind my clients that they are in the driver seat, and as a counsellor, I am in the passenger seat, meaning that there are no obligations, and I will go at your own pace. As a counsellor, it is my role to ask the right questions, even if you're uncertain about what specifically is bothering you. During a first counselling session, we will review informed consent and I will ask a variety of questions that will provide some guidance. Any questions you may have can be answered at this time, or at any point throughout counselling. Building a strong therapeutic relationship is vital for successful therapy, and I understand that different clients have different preferences. Some clients prefer uninterrupted self-expression, while others appreciate more structure or guidance. Your session will be tailored to your preferences and what makes you comfortable. Ultimately, in the first session, I want to help you feel as comfortable as possible and get to know you better!",
        },
        {
            question: "What can I expect from the consultation call?",
            answer: "The consultation call gives you an opportunity for you to ask any questions you might have, gain insights into my counselling approach, and ensure a good match between you and me. (Numerous academic studies on effective counselling consistently highlight the importance of the client-therapist relationship as a major factor in achieving success.) During our conversation, I'll share my counselling approach and give you a clear picture of what you can expect if you choose to work with me. Additionally, I will inquire about what has brought you to counselling and what you hope to achieve. From the call, my hope is that you will be able to make an informed decision about whether you would like to book a full session with me.",
        },
        {
            question: "What is your approach to therapy?",
            answer: "My approach is rooted in a variety of evidence-based modalities, including attachment-based therapy, emotion-focused therapy, internal family systems, person-centered therapy and trauma-informed care. I tailor my therapy approach to each client based on their unique needs, experiences and goals.  I actively encourage clients to voice their questions, concerns and provide feedback throughout the therapeutic process in order to meet their goals and needs. Part of my job is to help clients develop a deeper understanding of themselves, their relationships, and their experiences, and to provide them with the tools and strategies they need to achieve their goals and live more fulfilling lives.",
        },
        {
            question: "How much does a counselling session cost?",
            answer: "$140.00 NZD for a 50 minute counselling session & $210.00 NZD for a 75 minute counselling session.",
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
            question: "What can I gain from counselling?",
            answer: "Speaking freely in a safe and truly non-judgemental atmosphere is designed to be therapeutic, and can enable you to face and embrace your truths.  While confiding in a friend or family member can be valuable, consulting with a qualified therapist provides distinct advantages. Therapists bring expertise, offering diverse perspectives and the necessary tools to tackle your specific challenges. We actively listen, ensuring an unbiased viewpoint and providing feedback. As you work with the right counsellor, you'll gradually develop comfort and confidence in the process. This growth allows for deeper exploration of emotions, leading to clarity in identifying and addressing problems. Counsellors often reframe situations, helping you uncover your own solutions. Many individuals report an array of valuable outcomes from the counselling process, a few include: healthier relationships with self and others, increased self-awareness, self-esteem and the adoption of positive coping strategies.",
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
            answer: "The number of counselling sessions varies for each individual and situation, as there is no set formula. We will collaboratively consider your unique circumstances when determining the frequency and duration of sessions. While acute issues or crises may require regular sessions for a shorter period, many clients transition to less frequent appointments, to sustain their mental health and well-being. This journey is highly personalised, and together we will create a tailored plan based on your goals, needs, and available resources.",
        },
        {
            question: "I have other questions for you, how can I reach you?",
            answer: "If you have any further questions about anything at all, please contact me via my email at beckybradleycounselling@gmail.com, the contact form below, or book a free consultation call.",
        },
        {
            question: "I’ve decided to come to therapy, now what?",
            answer: "You can email me at beckybradleycounselling@gmail.com or use the Book Now button to schedule a consultation or counselling session. I look forward to hearing from you!",
        },
    ];
</script>

<header
    bind:clientHeight={headerHeight}
    class={"duration-200 sticky top-0 relative border-b border-solid  " +
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
            <img src="/profile2.png" alt="profile-img" />
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
        <p
            class="text-sm sm:text-base max-w-[700px] mx-auto w-full text-center"
        >
            I am a Counsellor based in Auckland, New Zealand. Having had the
            privilege of growing up in six countries, I have a deep appreciation
            for diverse identities, cultures and backgrounds. When I'm not
            outdoors, playing board games or enjoying time with loved ones, I'm
            dedicated to making quality therapy accessible to all. Through my
            personal journey, I've witnessed firsthand the incredible impact
            therapy can have. Join me on this empowering path towards positive
            change. My areas of practice include:
        </p>
        <div
            class="flex items-center flex-wrap gap-2 sm:gap-4 max-w-[700px] mx-auto w-full justify-center"
        >
            {#each [...keyWords].sort() as keyWord}
                <div
                    class={" py-2 rounded text-xs sm:text-base px-3 text-white sm:flex-1 text-center " +
                        ["bg-indigo-600", "bg-indigo-500", "bg-indigo-400"][
                            Math.floor(Math.random() * 3)
                        ]}
                >
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
                <div
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
                </div>
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
        <div
            class="flex flex-col gap-4 select-none max-w-[800px] mx-auto w-full"
        >
            {#each faq as question, questionIndex}
                <button
                    on:click={() => {
                        if (displayFAQ.includes(questionIndex)) {
                            displayFAQ = displayFAQ.filter(
                                (val, valIndex) => val !== questionIndex
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
        <div class="flex items-center ">
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
            href="https://www.linkedin.com/in/jamezmcarthur/"
            target="_blank">Website by James Development</a
        >
    </div>
</footer>

<svelte:window bind:scrollY={y} />
