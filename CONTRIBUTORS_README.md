The two sudoku SVG's are from Wikipedia: https://en.wikipedia.org/wiki/Sudoku

Copying the Contributor's style guide from the [rfc](https://github.com/bevyengine/rfcs/blob/main/rfcs/23-quick_start_book.md):

### Contributor's style guide

When writing and reviewing learning material for the Bevy Book and Quick Start Games, please try to follow these guidelines:

#### Writing

1. Use clear, simple language.
2. Prefer short sentences. Remove extra words.
3. **Bold** new vocabulary words where they are defined.
   1. Define them as soon as is reasonable after they are introduced.
4. Make sure your grammar and spelling are correct.
5. Avoid idioms and slang.
6. Speak directly to the reader in an approachable tone. Use "we" and "you" pronouns.
7. It can be useful to create specific, named characters to demonstrate a point.
   1. If you do, pick a pronoun set for them and stick to it.
   2. Otherwise, use  "they/them" third-person pronouns to refer to the reader or others.
8. Keep humor light.
   1. Avoid off-color or offensive humor.
   2. Be mindful not to overuse in-jokes or cultural references.
   3. Don't drag your jokes out: that's not what the audience is here to read.

#### Organizational

1. Carefully organize your work into separate pages, headings, paragraphs and code blocks.
2. Clearly signal when you are explaining a concept in technical depth so it can be skipped.
3. Use lists, numbered lists and sub-lists to present information in bite-sized ways.
   1. Refer back to these items by number!
4. Provide plenty of links, but be sure that what you are linking to is obvious by context.
   1. Link to other sections of the book / example / web page when you mention them.
   2. Always link to the most specific location you can, whether that's a section on a page or a method on a struct.
   3. Use the `latest` tag when linking to Bevy docs and source code so it won't go stale every time the version is updated.
   4. When linking to detailed explanations or discussions, summarize the most important points in addition to providing a link.

#### Technical

1. All examples must be able to be compiled and run.
2. Prefer game-relevant, descriptive examples and variable names over generic ones like `MyEvent`. Avoid meaningless names like `foo` at all times.
3. It's good practice to break your code into blocks with comments or explanatory text, but you need to link to a cohesive, copy-able whole at the end.
4. Examples must pass Bevy's standard `clippy` lints.
5. The polish level of your examples should correspond to the point you're trying to make.
   1. If you're demonstrating a new feature, show only the most basic syntax as locally as possible.
   2. When trying to explain how a game can be made, organize and polish your code to showcase best practices.
   3. Lack of polish should serve an end: don't show bad or sloppy practices without a good reason.
   4. Showing how (and why!) to refactor your code is a very powerful teaching tool.
6. Stick to a consistent style (e.g. for loops vs map) within each example.
7. If you need to give advice that will only matter to some of your audience (e.g. how to handle an edge case, or support a specific platform), do so in a clearly marked aside or list.
8. Examples should not use or rely on third-party plugins.
These may be appropriate to link in "next steps" however at the end of the examples.
   1. Third-party crates should be limited to the most essential, such as `rand`.

## Implementation strategy

1. The user-facing explanation above should live in `CONTRIBUTING.md` of the [`bevy-website` repo](https://github.com/bevyengine/bevy-website).
2. This should be linked to from the website, likely under a "Contributing" tab.
3. Per [bevy-website #143](https://github.com/bevyengine/bevy-website/issues/143),the website will need to be revamped somewhat.
4. Automatic compilation of code snippets is the critical feature from the above, ensuring that we can keep the examples current in a reliable way.
5. Once this RFC is merged, work should begin on a separate branch of `bevy-website` repo to create a new book.
6. For the launch of 0.6 (or perhaps sooner), this branch is merged and becomes the new `main`.
7. A persistent `bevy-main` branch of the repo is maintained and with a dependency on the `main` branch of `bevy` to ensure that we can test out new changes and refine the code before new features and breaking changes go live and reduce release crunch.


