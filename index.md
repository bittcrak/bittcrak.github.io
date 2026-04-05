---
layout: default
title: main()
---

<style>
.terminal-line {
  margin-bottom: 8px;
}

.prompt {
  color: #b5e853;
}

.prompt-user {
  color: #63c0f5;
}

.prompt-path {
  color: #aa759f;
}

.command {
  color: #ebdbb2;
}

.output {
  color: #928374;
  margin-left: 0;
  margin-bottom: 14px;
}

.output-muted {
  color: #888;
}

.terminal-input-line {
  display: flex;
  align-items: center;
}

#terminal-input {
  background: transparent;
  border: none;
  color: #ebdbb2;
  font-family: inherit;
  font-size: 16px;
  outline: none;
  flex: 1;
  caret-color: #b5e853;
}
</style>

<div class="terminal-line output-muted">MeowOS 12.0.1-amd64 x86_64 GNU/Linux</div>
<div class="terminal-line output-muted">Type 'help' for help.</div>
<div class="terminal-line" style="margin-top: 16px;"></div>
<div id="terminal-output"></div>
<div class="terminal-input-line">
  <span class="prompt"><span class="prompt-user">user</span>@<span class="prompt-path">tinkerer</span>:~$&nbsp;</span>
  <input type="text" id="terminal-input" autofocus autocomplete="off" spellcheck="false">
</div>

<script>
const commands = {
  help: `Available commands:
whoami      - who is bittcrak?
ping        - How to reach me
ps          - Blogs topics
clear       - Clear term`,

  banner: `I'm <span style="color:#63c0f5">Devansh</span>, I also go by bittcrak online!! I am trying to get 'crakd'(meaning I want to get better)

wannabe security researcher, currently somewhere in the middle of the pipeline; I believe in:
- Human Curiosity can never be replaced with AI Efficiency
- Malwares are peak software engineering
- Exploit Development is peak problem solving
- Reverse Engineering is peak discipline
- Maths is required skill for getting cracked`,

  ps: `Technical Skills:
- Fast Learner
- Reverse Engineering
- Binary Exploitation 
- Malware Analysis
- Scripting & Programming
- CTFs`,

 ping: `Find me at:
- <a href="https://github.com/bittcrak" style="color:#63c0f5">Github</a>
- <a href="https://linkedin.com/bittcrak" style="color:#63c0f5">Linkedin</a>
`,

  cat: `Sometimes I dump information that I found interesting in case some lonely scholar happens to cross paths.

They are in <span style="color:#63c0f5">/blogs</span> section in the nav bar.

Topics include:
- Challenges from CTF's HTB and such
- Rabbit hole deep dives`,

  clear: 'CLEAR'
};

const terminalOutput = document.getElementById('terminal-output');
const terminalInput = document.getElementById('terminal-input');
const terminal = document.getElementById('main_content');

function addOutput(cmd, output) {
  const cmdLine = document.createElement('div');
  cmdLine.className = 'terminal-line';
  cmdLine.innerHTML = `<span class="prompt"><span class="prompt-user">guest</span>@<span class="prompt-path">tinkerer</span>:~$&nbsp;</span><span class="command">${cmd}</span>`;
  terminalOutput.appendChild(cmdLine);

  if (output !== 'CLEAR') {
    const outputDiv = document.createElement('div');
    outputDiv.className = 'terminal-line output';
    outputDiv.innerHTML = output.replace(/\n/g, '<br>');
    terminalOutput.appendChild(outputDiv);
  }
}

function processCommand(cmd) {
  const trimmed = cmd.trim().toLowerCase();
  
  if (trimmed === '') return;
  
  if (trimmed === 'clear') {
    terminalOutput.innerHTML = '';
    return;
  }

  const output = commands[trimmed] || `Command not found: ${cmd}. Type 'help' for help`;
  addOutput(cmd, output);
  
  terminal.scrollTop = terminal.scrollHeight;
}

terminalInput.addEventListener('keydown', (e) => {
  if (e.key === 'Enter') {
    processCommand(terminalInput.value);
    terminalInput.value = '';
  }
});

// Focus input when clicking anywhere in terminal
terminal.addEventListener('click', () => terminalInput.focus());
</script>
