<form
    name="contact"
    method="POST"
    class="flex flex-col gap-4 max-w-[500px] w-full mx-auto text-slate-800 text-xs sm:text-sm"
    action="https://formsubmit.co/beckybradleycounselling@gmail.com"
>

    <input
        name="name"
        type="text"
        placeholder="Full Name"
        class="outline-none focus:outline none bg-white p-2 rounded border-2 border-solid border-transparent hover:border-indigo-200 focus:border-indigo-200 duration-200"
    />
    <input
        required
        name="email"
        type="email"
        placeholder="Email Address"
        class="outline-none focus:outline none bg-white p-2 rounded border-2 border-solid border-transparent hover:border-indigo-200 focus:border-indigo-200 duration-200"
    />
    <input
        name="subject"
        type="text"
        placeholder="Subject"
        class="outline-none focus:outline none bg-white p-2 rounded border-2 border-solid border-transparent hover:border-indigo-200 focus:border-indigo-200 duration-200"
    />
    <textarea
        required
        name="message"
        placeholder="Your message"
        class="outline-none focus:outline none bg-white p-2 rounded border-2 border-solid border-transparent hover:border-indigo-200 focus:border-indigo-200 duration-200 h-32 resize-none"
    />
    <button
        type="submit"
        class="border-white border-solid border-[1.5px] text-white px-4 py-2 rounded duration-200 hover:border-indigo-200"
        >Submit</button
    >
</form>
