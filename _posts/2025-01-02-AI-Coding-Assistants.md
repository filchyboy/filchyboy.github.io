# Today

* I have been experimenting with coding assistants like [Github Copilot](https://github.com/features/copilot), [Windsurf](https://codeium.com/windsurf), and [Cursor](https://www.cursor.com/). I see how they can be valuable. But they are also problematic for the same reasons I have discussed previously. If you know a topic well, then LLMs can be helpful. If you do not, it can be incredibly easy to be waylaid by an LLM that took a wrong turn, which you overlooked.

* My main takeaway from experimenting with these assistants is that I feel pushed towards even greater clarity in what I am building. The more precise I am with my requirements, the better the assistant performs, and the less likely I am to stumble down a bad path and have to figure it out too late.

* I found a couple of great resources for understanding some of the complexities around developing with Cursor. These two pieces by [Prajwal Tomar](https://x.com/prajwaltomar_/status/1874461570740420945) and [*Mastering Long Codebases with Cursor, Gemini, and Claude: A Practical Guide*](https://forum.cursor.com/t/mastering-long-codebases-with-cursor-gemini-and-claude-a-practical-guide/38240/1) by Wheattoast11.

## Cursor AI

### Guidelines

1/ Plan Before Coding

- Always start with a solid plan. Use ChatGPT to create your PRD, database design, color palette, and structure. Save these as .md files in Cursor to keep everything consistent. A clear roadmap saves time.

2/ Start with a Strong Foundation

- Cursor shines when it’s building on something. Use tools like V0 to generate the initial UI code, then refine it in Cursor. This approach improves accuracy and reduces rework.

3/ Use [cursor.directory](https://github.com/pontusab/cursor.directory) for Better Prompts

- Leverage tech-specific prompts from [Cursor’s directory](https://cursor.directory/). Customize them for your project using a `.cursorrules` file to improve precision, especially for your stack.

4/ Tag Relevant Docs

- Sync official docs (Next.js, Supabase, etc.) into Cursor. Reference popular libraries using @LibraryName, or add your own using @Docs → Add new doc.

5/ Ask the Web

-	Get up-to-date information from the internet with @Web. Cursor will search the web for you and use the latest information to answer your question.

6/ Save Working Code in .md Files

- Save good code from Cursor in `.md` files for future reference. It speeds up future responses and ensures you always have examples to reuse.

7/ Query the Entire Codebase

- Use @Codebase to ask questions about your project. Cursor will search and respond based on the entire codebase.

8/ Fast Edits

- Edit and write code with the AI. Select some code, click `⌘ K`, and describe how the code should be changed. Or, generate new code with `⌘ K` without selecting anything.

9/ Use Images for Visual Feedback

- Not happy with your UI? Take a screenshot, click the image button under the chat, or drag the image into the input box to provide visual context.

10/ Use AI to Explain Code

- Learning while building? Ask Cursor to explain your code like you’re a beginner. Over time, you’ll see clearer coding patterns.

11/ Start with Code Templates

- Don’t reinvent the wheel. Use boilerplate code for common elements like auth, payments, or databases. Start fast with [proven templates](https://vercel.com/templates/next.js).

### Key Takeaway:

1. Cursor works best when you provide clear and detailed prompts.

2. Set it up right, and you’ll save hours, avoid mistakes, and build FASTER than ever.


