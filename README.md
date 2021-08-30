<!--

author: André Dietrich

email: LiaScript@web.de

version: 0.0.2

logo: https://upload.wikimedia.org/wikipedia/commons/thumb/0/0a/The_Great_Wave_off_Kanagawa.jpg/1280px-The_Great_Wave_off_Kanagawa.jpg

comment: Demo on dynamically creating LiaScript-content by using scripts. Furthermore it is demonstrated how macros can be combined to create more engaging courses.

test: @Textanalysis.FULL

import: https://raw.githubusercontent.com/liaTemplates/TextAnalysis/main/README.md

imageDescriber
Image: <script input="text" update-on-change="false" output="url">
let url = "@input"

// if no output has been defined then output a default string "load"
// this string is published at the topic "url"
if (url === "") {
  "@0"
} else {
  url
}
</script>


Select option:
<script output="mode" input="select" value="Picture" options="Picture|Graph|Code">
// publish the user selection directly as a string
"@input"
</script>

The following script generates the entire user input

<script modify="false" run-once="true">
// receive the input from the topic url
let url = "@input(`url`)"

// ok, this is a required to prevent wrong inputs atm
if (url === "load" || url.startsWith("@input(")) {
  ""
} else {
  // This is where all the magic happens, it simply grabs the input from
  // the output from topic mode and returns 3 different LiaScript code
  // elements. `send.liascript` forces the content to be parsed by LiaScript.
  switch ("@input(`mode`)") {
    case "Picture": {
      send.liascript(`![](${url})

Attention
=========

To capture the attention of your readers, you should start with a good introduction phrase(s).

Here are some examples you may use:

* If you look at this picture, you will see...
* In the picture you can see...
* The picture shows...

\`\`\` text
please enter som text
\`\`\`
@test


more Stuff
==========

Now that we have the attention of your reader, and we have a general understanding on what is been displayed, you should start looking at details.

Here are some examples on how to continue:

* The image we are looking at has been painted/taken at...
* When you look at the image, you can see that it is a black and white...
* This picture is a... picture and has been taken by...

\`\`\` text
please enter som text
\`\`\`
<script>
console.log(\`beautifull -> @'input\`)
"LIA: stop"
</script>


more Stuff 2
============


Okay... we should now have finished the introduction of your description.

So, now please describe the picture and use phrases like:

* In the foreground of the picture you will...
* In the background you can see that...
* In the right/left/center...
* Between ... there is ...
* At the top/At the bottom there is...

\`\`\` text
please enter som text
\`\`\`
<script>
console.log(\`beautifull -> @'input\`)
"LIA: stop"
</script>

`)
      break
    }
    case "Graph": {
      send.liascript(`![](${url})

Graph: todo
=====
`)
      break
    }
    case "Code": {
      send.liascript(`![](${url})

Code: todo
=====
`)

      break
    }
  }
}
</script>
@end


-->

# Image-Describer

This is only a demo, which shows, how 3 different scripts can be combined. It
furthermore makes use of the
[TextAnalysis-Template](https://github.com/LiaTemplates/TextAnalysis), which can
be used to perform standard style analysis on some input text.

<!--style="display:none"-->
You can try it out on LiaScript: https://LiaScript.github.io/course/?https://github.com/LiaPlayground/ImageDescriber/blob/main/README.md

---

The first is simply an input for a text. By clicking onto this `load` element you can insert and image url, for example the following one:

`https://upload.wikimedia.org/wikipedia/commons/thumb/0/0a/The_Great_Wave_off_Kanagawa.jpg/1280px-The_Great_Wave_off_Kanagawa.jpg`

**Image: <script input="text" update-on-change="false" output="url">
let url = "@input"

// if no output has been defined then output a default string "load"
// this string is published at the topic "url"
if (url === "") {
  "load"
} else {
  url
}
</script>**

---

Within the following selection it is possible to select three different options `Picture|Graph|Code`, `Picture` is selected by default.

**Select option: <script output="mode" input="select" value="Picture" options="Picture|Graph|Code">
// publish the user selection directly as a string
"@input"
</script>**

---

The following script generates the entire user input based on the published
values from the both scripts above. Whenever the inputs from the above examples
are passed via the `@input(\`topic\`)` macro, which gets substituted on every
change.


<script modify="false" run-once="true">
// receive the input from the topic url
let url = "@input(`url`)"

// ok, this is a required to prevent wrong inputs atm
if (url === "load" || url.startsWith("@input(")) {
  ""
} else {
  // This is where all the magic happens, it simply grabs the input from
  // the output from topic mode and returns 3 different LiaScript code
  // elements. `send.liascript` forces the content to be parsed by LiaScript.
  switch ("@input(`mode`)") {
    case "Picture": {
      send.liascript(`![](${url})

Attention
=========

To capture the attention of your readers, you should start with a good introduction phrase(s).

Here are some examples you may use:

* If you look at this picture, you will see...
* In the picture you can see...
* The picture shows...

\`\`\` text
please enter som text
\`\`\`
@test


more Stuff
==========

Now that we have the attention of your reader, and we have a general understanding on what is been displayed, you should start looking at details.

Here are some examples on how to continue:

* The image we are looking at has been painted/taken at...
* When you look at the image, you can see that it is a black and white...
* This picture is a... picture and has been taken by...

\`\`\` text
please enter som text
\`\`\`
@test


more Stuff 2
============


Okay... we should now have finished the introduction of your description.

So, now please describe the picture and use phrases like:

* In the foreground of the picture you will...
* In the background you can see that...
* In the right/left/center...
* Between ... there is ...
* At the top/At the bottom there is...

\`\`\` text
please enter som text
\`\`\`
@test

`)
      break
    }
    case "Graph": {
      send.liascript(`![](${url})

Graph: todo
=====
`)
      break
    }
    case "Code": {
      send.liascript(`![](${url})

Code: todo
=====
`)

      break
    }
  }
}
</script>

## Examples

The header of this document contains a macro, which does actually the same as
the previous example, but by using the macros, which perform only a basic form
of textsubstitution, you load the same functionality multiple times.

### Empty settings

> Load an empty example, where the user still has to chose an image her/himself.

@imageDescriber(load)

### Preset image

> Preset the image an thus also display the inputs from the third script.

@imageDescriber(https://upload.wikimedia.org/wikipedia/commons/thumb/0/0a/The_Great_Wave_off_Kanagawa.jpg/1280px-The_Great_Wave_off_Kanagawa.jpg)

### Overwrite test-macro
<!--
test: @Textanalysis.full
-->

> Preset the image and replace the default testing method by `@Textanalysis.full`:

@imageDescriber(https://upload.wikimedia.org/wikipedia/commons/thumb/0/0a/The_Great_Wave_off_Kanagawa.jpg/1280px-The_Great_Wave_off_Kanagawa.jpg)
