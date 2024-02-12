# Lab Report 3
## Part 1

A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown)

```
@Test
  public void testAverageWithoutLowestRepeat() {
    double[] input1 = {1, 2, 1};
    assertEquals( 1.5, ArrayExamples.averageWithoutLowest(input1), 0.001);
  }
```

An input that doesn't induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown)

```
@Test
  public void testAverageWithoutLowest2() {
    double[] input1 = {1, 2};
    assertEquals( 2, ArrayExamples.averageWithoutLowest(input1), 0.001);
  }
```
The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)
![Image](https://github.com/efang5/cse15l-lab-reports/blob/main/Screenshot%202024-02-10%20at%207.31.03%20PM.png?raw=true)

The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown)

Before
```
static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest)
      {
        sum += num;
      }
    }
    return sum / (arr.length - 1);
  }
```
After
```
static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      sum += num;
    }
    sum -= lowest;
    return sum / (arr.length - 1);
  }
```

## Part 2
Chosen: find

Method 1 - fd
```

```
Method 2 - locate
```
$ locate terminal/
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/LICENSE
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/common
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/common/base-terminal-protocol.js
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/common/shell-terminal-protocol.js
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/common/terminal-common-module.js
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/common/terminal-protocol.js
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/common/terminal-watcher.js
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/node
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/node/base-terminal-server.js
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/node/buffering-stream.js
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/node/index.js
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/node/shell-process.js
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/node/shell-terminal-server.js
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/node/terminal-backend-contribution.js
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/node/terminal-backend-contribution.slow-spec.js
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/node/terminal-backend-module.js
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/lib/node/terminal-server.js
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/package.json
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/src
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/src/browser
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/src/browser/search
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/src/browser/search/terminal-search-widget.tsx
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/src/browser/style
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/src/browser/style/terminal-search.css
/Applications/Arduino IDE.app/Contents/Resources/app/node_modules/@theia/terminal/src/browser/style/terminal.css
/Applications/PyCharm CE.app/Contents/plugins/python-ce/helpers/typeshed/stubs/humanfriendly/humanfriendly/terminal/__init__.pyi
/Applications/PyCharm CE.app/Contents/plugins/python-ce/helpers/typeshed/stubs/humanfriendly/humanfriendly/terminal/html.pyi
/Applications/PyCharm CE.app/Contents/plugins/python-ce/helpers/typeshed/stubs/humanfriendly/humanfriendly/terminal/spinners.pyi
/Applications/PyCharm CE.app/Contents/plugins/python-ce/helpers/typeshed/stubs/stripe/stripe/api_resources/terminal/__init__.pyi
/Applications/PyCharm CE.app/Contents/plugins/python-ce/helpers/typeshed/stubs/stripe/stripe/api_resources/terminal/connection_token.pyi
/Applications/PyCharm CE.app/Contents/plugins/python-ce/helpers/typeshed/stubs/stripe/stripe/api_resources/terminal/location.pyi
/Applications/PyCharm CE.app/Contents/plugins/python-ce/helpers/typeshed/stubs/stripe/stripe/api_resources/terminal/reader.pyi
/Applications/PyCharm CE.app/Contents/plugins/terminal/lib
/Applications/PyCharm CE.app/Contents/plugins/terminal/lib/terminal.jar
/Applications/PyCharm CE.app/Contents/plugins/terminal/pwsh
/Applications/PyCharm CE.app/Contents/plugins/terminal/pwsh/pwsh.ps1
/Applications/PyCharm CE.app/Contents/plugins/terminal/shell-integrations
/Applications/PyCharm CE.app/Contents/plugins/terminal/shell-integrations/bash
/Applications/PyCharm CE.app/Contents/plugins/terminal/shell-integrations/bash/bash-integration.bash
/Applications/PyCharm CE.app/Contents/plugins/terminal/shell-integrations/bash/command-block-support.bash
/Applications/PyCharm CE.app/Contents/plugins/terminal/shell-integrations/fish
/Applications/PyCharm CE.app/Contents/plugins/terminal/shell-integrations/fish/command-block-support.fish
/Applications/PyCharm CE.app/Contents/plugins/terminal/shell-integrations/fish/fish-integration.fish
/Applications/PyCharm CE.app/Contents/plugins/terminal/shell-integrations/powershell
/Applications/PyCharm CE.app/Contents/plugins/terminal/shell-integrations/powershell/command-block-support.ps1
/Applications/PyCharm CE.app/Contents/plugins/terminal/shell-integrations/powershell/powershell-integration.ps1
/Applications/PyCharm CE.app/Contents/plugins/terminal/zsh
/Applications/PyCharm CE.app/Contents/plugins/terminal/zsh/.zshenv
/Applications/PyCharm CE.app/Contents/plugins/terminal/zsh/hooks.zsh
```

Method 3 - fzf

Method 4 - ffind
