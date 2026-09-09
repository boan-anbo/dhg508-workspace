# Week 2

Before our next class.

## Tasks

Use your own fork of the course workspace. Ask OpenCode to help you bring it up
to date and open it in VS Code.

For LLM-based OCR, use one of these APIs. Give OpenCode the official guide and
ask it to help you use a model that accepts images:

- OpenRouter: https://openrouter.ai — [image-input guide](https://openrouter.ai/docs/guides/overview/multimodal/image-understanding)
- DeepSeek: https://platform.deepseek.com — [vision API guide](https://api-docs.deepseek.com/guides/vision/)

## Challenges

Do these through OpenCode. Tell it what you want to find out and ask it to
explain what it is doing. Check its work against your sources.

### 1. Choose a historical question

Answer one question about anything **before 1950**, preferably connected to
your interests. For example:

- When was Lingnan University founded?
- When did Peking University first admit women?
- When did the first railway in China begin operating?

### 2. Find two pieces of evidence

Find **at least two pieces of evidence from two credible sources**, using the
open Internet or academic databases. Keep the links or references.

**Evaluate the evidence, not just the website.** “PKU's website says so” is not
sufficient evidence by itself. Find the records or documents supporting the
claim and explain why they support your answer. Does “admitting women,” for
example, mean allowing them to attend classes or formally enrolling them?

### 3. OCR at least one source

At least **one source must need OCR**: a scan or photograph whose text has not
yet been converted into machine-readable text.

Ask OpenCode to help you try these methods **in this order**:

1. **Start with an LLM API:** OpenRouter or DeepSeek, using the guides above.
2. **Then try the PaddleOCR API** if the first result needs improvement.
3. **As a last resort, use OpenCode's own vision capabilities.**

You do not need to try all three if an earlier method works well. Check the
output against the original image. If you try more than one method, compare
the results and choose the one that works best for your source. Use the
checked text to support your answer.

### 4. Save your work and push it back

In your fork, create `assignments/week-02/answer.md`. Keep it short: your
question and answer, your two pieces of evidence and why they are reliable,
and how you did the OCR—including any useful tricks or problems.

Use a project under `projects/` for your research (see the
[workspace guide](../../WORKSPACE.md)). Keep its original source images
unchanged in `sources/raw/` and the OCR text in `sources/processed/`. Link to
these from your answer so you can show them in class.

Commit your answer and small supporting files, then push to your own GitHub
account. Keep large files and API keys out of Git. Add unresolved questions
to your existing `questions.md`.

## Bring to class

Be ready to:

1. **Tell us your question and your answer.**
2. **Show your two pieces of evidence** and explain why you consider the sources reliable.
3. **Explain how you OCRed at least one source.** Show the original and the OCR result, explain which method you used, and share any useful tricks or problems you encountered.
