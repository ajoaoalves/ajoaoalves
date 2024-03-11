### Hi there 👋

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

import axios from "axios";
import fs from "fs";
import jsYaml from "js-yaml";

const LANGS_FILEPATH = "./src/common/languageColors.json";

//Retrieve languages from github linguist repository yaml file
//@ts-ignore
axios
  .get(
    "https://raw.githubusercontent.com/github/linguist/master/lib/linguist/languages.yml",
  )
  .then((response) => {
    //and convert them to a JS Object
    const languages = jsYaml.load(response.data);

    const languageColors = {};

    //Filter only language colors from the whole file
    Object.keys(languages).forEach((lang) => {
      languageColors[lang] = languages[lang].color;
    });

    //Debug Print
    //console.dir(languageColors);
    fs.writeFileSync(
      LANGS_FILEPATH,
      JSON.stringify(languageColors, null, "    "),
    );
  });
