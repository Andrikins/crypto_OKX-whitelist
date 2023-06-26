![icon](./icon.png)

## by [@ifrosta](https://github.com/iFrosta)
### Join [Telegram](https://t.me/+z9FiPTeuuMZjZjhi)
### Donate: ❤️  ``0xbB86A17094a1D03eF12418F63C9e0dd28BC511e1``


# How to use

1. Open [https://okx.com/balance/withdrawal-address](https://okx.com/balance/withdrawal-address)
2. Press on 'Add new address'
3. Select the withdrawal network
4. Open the console
5. Paste the script
6. [Fill](#-how-to-fill-wallets) the wallets with your wallets
7. (Optional) Script will get labels automatically Modify ``t`` and ``n`` if necessary
8. Press enter to run the script
9. Enjoy! ☺️

The script will tick the checkboxes and fill wallets.<br>
If there are more fields than wallets, script will remove unnecessary fields.

# How to fill wallets
```
let wallets = '
    0xbB86A17094a1D03eF12418F63C9e0dd28BC511e1 wallet-1
    0xbB86A17094a1D03eF12418F63C9e0dd28BC511e1 2 test wallet
    0xbB86A17094a1D03eF12418F63C9e0dd28BC511e1
    ...
'
```

```
let wallets=`

`,

t="",l="";

const o=!1;function n(wallets,t,l){const n=document.querySelectorAll(wallets)[t];o&&console.log("address",l,"Input",n),n&&(n.setAttribute("value",l),n.dispatchEvent(new Event("input",{bubbles:!0})))}async function s(){const wallets=document.querySelector(".add-address-form-btn");return wallets||(await a(50),s())}function a(wallets){return new Promise((t=>setTimeout(t,wallets)))}(async()=>{console.log((console.log(atob("   CiAgICAgICAgICBfICBfXyAgICAgICAgICAgICAgIF8gICAgICAgIAogICAgX19fXyAoXykvIF98ICAgICAgICAgICAgIHwgfCAgICAgICAKICAgLyBfXyBcIF98IHxfIF8gX18gX19fICBfX198IHxfIF9fIF8gCiAgLyAvIF9gIHwgfCAgX3wgJ19fLyBfIFwvIF9ffCBfXy8gX2AgfAogfCB8IChffCB8IHwgfCB8IHwgfCAoXykgXF9fIFwgfHwgKF98IHwKICBcIFxfXyxffF98X3wgfF98ICBcX19fL3xfX18vXF9fXF9fLF98CiAgIFxfX19fLyAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIA")),atob(["TWFkZSBieSBAaWZyb3N0YQpKb2luIGh0dHBzOi8vdC5tZS","8rejlGaVBUZXV1TVpqWmpoaQpEb25hdGUgMHhiQjg2QTE3","MDk0YTFEMDNlRjEyNDE4RjYzQzllMGRkMjhCQzUxMWUx"].join(""))));const i=function(){const t=wallets.includes("\t")?"\t":" ",l=wallets.trim().split("\n").map((wallets=>{const l=wallets.split(t);return{address:l[0],label:l.length>1?l.slice(1).join(" "):""}}));if(l.length<20)return console.log(`${l.length} Wallets`),l;return console.log(`${l.length} Wallets > 20, trim to 20 wallets\nLast wallet: ${l[19].address}`),l.slice(0,20)}();o&&console.log("Wallets:",i),""===t&&""===l&&function(){const wallets=document.querySelector(".withdraw-book-list");if(!wallets)return void console.log("Can't automatically find input labels");const n={address:"",label:""},s=wallets.querySelectorAll(".okui-form-item");let a=0;s.forEach((wallets=>{if(!(a>5)){if(2===wallets.classList.length&&wallets.classList.contains("okui-form-item-md")&&wallets.classList.contains("okui-form-item")){const t=wallets.querySelector(".okui-input-box");if(t){const wallets=t.querySelector(".okui-input-input");if(wallets){const t=wallets.getAttribute("placeholder");o&&console.log("Placeholder:",t),t&&(""===n.address?n.address=t:""===n.label&&(n.label=t))}}}a++}})),n.address&&n.label||console.log("Can't automatically find input labels");!n.address&&n.label||console.log(`Check auto generated labels\n\nAddress: ${n.address}\nLabel: ${n.label}`);t=n.address,l=n.label}(),await async function(wallets){const t=document.querySelectorAll(wallets);for(const wallets of t)wallets.checked||(o&&console.log(wallets,"click"),wallets.click()),await a(50)}(".okui-checkbox-input");const c=document.querySelector(".withdraw-book-list").querySelectorAll(".okui-form-item").length/5;c!==i.length&&(c<i.length?await async function(wallets){console.log(`Adding ${wallets.length-1} inputs..`);for(let t=0;t<wallets.length-1;t++){(await s()).click(),await a(100)}}(i):await async function(wallets){let t=document.querySelectorAll(".delete-address-btn");console.log("Removing inputs");for(;t.length!==wallets.length;){if(t.length>1){t[t.length-1].click()}await a(100),t=document.querySelectorAll(".delete-address-btn")}}(i)),await async function(wallets){for(const[o,s]of wallets.entries())console.log(`${parseInt(o+1,10).toString().padEnd(2)} wallet: ${s.address} ${s.label?`label: ${s.label}`:""}`),n(`.okui-input-input[placeholder="${t}"]`,o,s.address),s.label&&(await a(150),n(`.okui-input-input[placeholder="${l}"]`,o,s.label)),await a(150)}(i)})();
```

![GIF](./example.gif)

2023