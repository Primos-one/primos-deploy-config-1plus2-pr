# ⚠️ DEMONSTRATION KEYS ONLY — DO NOT USE FOR PRODUCTION ⚠️

These keys are public and embedded in the primos-deploy container.
Anyone can decrypt secrets encrypted with these keys.
For real projects, generate your own keys with: age-keygen

## Dev environment demo key
Public: age1zy8jc0jpsc2xs2wwq2nsn29h454fygsd9g6mv0mx750yldpvkucsh3zvz9

## How demo keys work
1. Demo private keys are ROT13-obfuscated inside the primos-deploy container
2. They are decoded in memory at runtime for sops decrypt
3. Private keys NEVER leave the container
4. Demo projects MUST have names starting with DEMO-DO-NOT-USE-

## Create a real project
primos-deploy project create-from-demo
