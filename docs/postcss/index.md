# POSTCSS

The tool itself is a Node.js module that parses CSS into an abstract syntax tree (AST); passes that AST through any number of “plugin” functions; and then converts that AST back into a string, which you can output to a file. Each function the AST passes through may or may not transform it; sourcemaps will be generated to keep track of any changes.

## Workflow

![workflow](../images/postcssWorkflow.png)

Core Structures:

- Tokenizer
- Parser
- Processor
- Stringifier

---

# References

[About POSTCSS](https://davidtheclark.com/its-time-for-everyone-to-learn-about-postcss/)
[Some things you may think about PostCSS... and you might be wrong](http://julian.io/some-things-you-may-think-about-postcss-and-you-might-be-wrong/)
