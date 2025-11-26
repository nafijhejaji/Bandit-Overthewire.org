# BANDIT overthewire.org
#In sha allah i'll remain consistent this time <br>


Bandit Level 2 → Level 3
🎯 Level Goal

Find the password stored inside a file with the name:

--spaces in this filename--


Located in the home directory.

❓ Problem

The filename contains spaces and starts with --, which looks like a command-line option.
If you run:

cat --spaces in this filename--


the shell interprets it as flags, not a file.

💡 Solution

Use quotes to handle spaces and ./ to force the shell to treat it as a file:

cat ./"--spaces in this filename--"

🧠 Why it works?

"--spaces in this filename--" → quotes allow spaces inside filenames

./ → ensures the command treats it as a file, not an argument like --spaces

Without these, Linux thinks you're passing options to cat

🔑 Password for next level:

MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
