![icon](./icon.png)

## by [@ifrosta](https://github.com/iFrosta)
### Join [Telegram](https://t.me/onchainsoft)
### Donate: ❤️  ``0xbB86A17094a1D03eF12418F63C9e0dd28BC511e1``


# How to use

1. Open [https://okx.com/balance/withdrawal-address](https://okx.com/balance/withdrawal-address)
1. Open the dev tools. (Ctrl + Shift + I)
2. Press Ctrl + Shift + R (prevent debugger pause)
2. Press on 'Add new address'
3. Select the withdrawal network
5. Paste the script
6. [Fill](#-how-to-fill-wallets) the wallets with your wallets
7. (Optional) Script will get labels automatically Modify ``t`` and ``o`` if necessary
8. Press enter to run the script
9. Enjoy! ☺️

The script will tick the checkboxes and fill wallets.<br>
If there are more fields than wallets, script will remove unnecessary fields.

# How to fill wallets
``` JavaScript
let wallets = '
    0xbB86A17094a1D03eF12418F63C9e0dd28BC511e1 wallet-1
    0xbB86A17094a1D03eF12418F63C9e0dd28BC511e1 2 test wallet
    0xbB86A17094a1D03eF12418F63C9e0dd28BC511e1
    ...
'
```

``` JavaScript
let wallets=`


`,

inputAddress="Address/domain",
inputLabel="e.g. my wallet",

run=async()=>{console.clear(),console.log(author());let e=getWallets(!0);e=e.slice(0,20),DEBUG&&console.log("Wallets:",e),""===inputAddress&&""===inputLabel&&getLabels(),await checkBoxForClick(FORM_CHECKBOX_SELECTOR);const t=countInputs();t!==e.length&&(t<e.length?await addInputs(e):await removeInputs(e)),await fillWallets(e),await setupDialogButtonListener(e),colorMsg("If everything is OK, press 'Save'","background-color: yellow; color: purple; font-size: 18px;")};const FORM_ADDRESS_LIST_SELECTOR=".withdraw-book-list",FORM_ITEM_SELECTOR=".balance_okui-form-item",FORM_ITEM_MD_SELECTOR=".balance_okui-form-item-md",FORM_CHECKBOX_SELECTOR=".balance_okui-checkbox",INPUT_BOX_SELECTOR=".balance_okui-input-box",INPUT_ADDRESS_SELECTOR=".balance_okui-input-input",INPUT_LABEL_SELECTOR=".balance_okui-input-input",INPUT_ERROR_SELECTOR=".balance_okui-form-item-control-explain-error",BUTTON_ADD_ADDRESS_SELECTOR=".add-address-form-btn",BUTTON_DELETE_ADDRESS_SELECTOR=".delete-address-btn",BUTTON_SAVE_SELECTOR_FIND=".balance_okui,balance_okui-btn,btn-sm,btn-fill-highlight,dialog-btn",OKX_TEXT_ADDRESS_DUPLICATE_ERROR="This address has already been saved, delete to save again as your chosen type";let BUTTON_SAVE_EL=null;const DEBUG=!1;let RESULT=!1,DUPLICATES=[];function colorMsg(e,t){console.log(`%c${e}`,t)}async function setupDialogButtonListener(e){const t=document.querySelectorAll(BUTTON_SAVE_SELECTOR_FIND),l=async()=>{DEBUG&&console.log("Save clicked"),await timeout(1200),await savedWalletsHandler(e)},o=Array.from(t).reverse();for(const e of o){const t=e.querySelector("span.btn-content");if(t&&"Save"===t.textContent.trim()){BUTTON_SAVE_EL=e,e.addEventListener("click",l);break}}}async function triggerSave(){BUTTON_SAVE_EL.parentElement.click()}async function fillWallets(e){for(const[t,l]of e.entries())console.log(`${parseInt(t+1,10).toString().padEnd(2)} wallet: ${l.address} ${l.label?`label: ${l.label}`:""}`),setInputValue(`${INPUT_ADDRESS_SELECTOR}[placeholder="${inputAddress}"]`,l.index?l.index:t,l.address),l.label&&(await timeout(150),setInputValue(`${INPUT_ADDRESS_SELECTOR}[placeholder="${inputLabel}"]`,l.index?l.index:t,l.label)),await timeout(150)}function setInputValue(e,t,l){const o=document.querySelectorAll(e)[t];DEBUG&&console.log("address",l,"Input",o),o&&(o.setAttribute("value",l),o.dispatchEvent(new Event("input",{bubbles:!0})))}async function addInputs(e){console.log(`Adding ${e.length-1} inputs..`);for(let t=0;t<e.length-1;t++){(await getAddBtn()).click(),await timeout(100)}}async function removeInputs(e){let t=document.querySelectorAll(BUTTON_DELETE_ADDRESS_SELECTOR);for(console.log("Removing inputs");t.length!==e.length;){if(t.length>1){t[t.length-1].click()}await timeout(100),t=document.querySelectorAll(BUTTON_DELETE_ADDRESS_SELECTOR)}}async function savedWalletsHandler(e){const t=getWallets(),l=await getDuplicatedWallets()||[];if(l.length){colorMsg("Please wait while doing post check..","background-color: yellow; color: purple; font-size: 18px;");const o=[],n=t.reduce(((t,n,a)=>(l.includes(n.address)?o.push(a):e.includes(n.address)||DUPLICATES.includes(n.address)||t.push({...n,index:t.length}),t)),[]);l.length&&DUPLICATES.push(...l.flat()),DEBUG&&(console.log("Duplicated Wallets:",l.length,l),console.log("Rest of Wallets:",n.length,n),console.log("DUPLICATES",DUPLICATES));const a=n.filter((e=>!DUPLICATES.includes(e.address)));if(DUPLICATES.length==t.length)return colorMsg("All wallets already added to whitelist on this chain","color: red; font-size: 14px;"),end();l.length&&a.length?(colorMsg("Sorting duplicates..","color: yellow; font-size: 14px;"),console.log("Replacing already saved wallets",a.length),await fillWallets(a),await timeout(800),await removeDuplicatedWallets(),await timeout(500),await triggerSave(a),await timeout(1200),await savedWalletsHandler(t)):l.length&&!n.length&&removeDuplicatedWallets()}end()}function end(){RESULT||(colorMsg("Done","color: #90EE90; font-size: 18px; font-weight: bold"),console.log(author()),RESULT=!0)}async function getDuplicatedWallets(){const e=OKX_TEXT_ADDRESS_DUPLICATE_ERROR,t=[],l=document.querySelectorAll(INPUT_ERROR_SELECTOR);if(l)return l.forEach((async l=>{if(l.textContent.trim()===e){const e=l.closest(FORM_ITEM_MD_SELECTOR).querySelector(INPUT_ADDRESS_SELECTOR),o=e?e.value:"";DEBUG&&console.log("Duplicate address value:",o),t.push(o)}})),t}async function removeDuplicatedWallets(){DEBUG&&console.log("Removing already saved wallets");const e=OKX_TEXT_ADDRESS_DUPLICATE_ERROR,t=document.querySelectorAll(INPUT_ERROR_SELECTOR),l=[];for(const o of t)if(o.textContent.trim()===e){const e=o.closest(FORM_ITEM_MD_SELECTOR),t=document.querySelectorAll(FORM_ITEM_MD_SELECTOR),n=Array.from(t).indexOf(e);if(n>=2){const e=t[n-2].querySelector(BUTTON_DELETE_ADDRESS_SELECTOR);e&&(DEBUG&&console.log("Removed already saved addresses",e),l.push(n-2))}}for(let e=l.length-1;e>=0;e--){const t=l[e],o=document.querySelectorAll(FORM_ITEM_MD_SELECTOR);if(t>=0&&t<o.length){const e=o[t].querySelector(BUTTON_DELETE_ADDRESS_SELECTOR);e&&(e.click(),await timeout(100))}}}async function getAddBtn(){const e=document.querySelector(BUTTON_ADD_ADDRESS_SELECTOR);return e||(await timeout(50),getAddBtn())}function btnClick(e,t=0){document.querySelectorAll(e)[t].click()}async function checkBoxForClick(e){const t=document.querySelectorAll(e);for(const e of t)e.checked||(DEBUG&&console.log(e,"click"),e.click()),await timeout(50)}function getLabels(){const e=document.querySelector(FORM_ADDRESS_LIST_SELECTOR);if(!e)return void console.log("Can't automatically find input labels");const t={address:"",label:""},l=e.querySelectorAll(FORM_ITEM_SELECTOR);let o=0;return l.forEach((e=>{if(!(o>5)){if(2===e.classList.length&&e.classList.contains(FORM_ITEM_MD_SELECTOR.replace(".",""))&&e.classList.contains(FORM_ITEM_SELECTOR.replace(".",""))){const l=e.querySelector(INPUT_BOX_SELECTOR);if(l){const e=l.querySelector(INPUT_ADDRESS_SELECTOR);if(e){const l=e.getAttribute("placeholder");DEBUG&&console.log("Placeholder:",l),l&&(""===t.address?t.address=l:""===t.label&&(t.label=l))}}}DEBUG&&console.log("MD",e.classList.contains(FORM_ITEM_MD_SELECTOR.replace(".",""))),DEBUG&&console.log("ITEM",e.classList.contains(FORM_ITEM_SELECTOR.replace(".",""))),o++}})),t.address&&t.label||console.log("Can't automatically find input labels"),!t.address&&t.label||console.log(`Check auto generated labels\n\nAddress: ${t.address}\nLabel: ${t.label}`),inputAddress=t.address,inputLabel=t.label,!0}function countInputs(){return document.querySelector(FORM_ADDRESS_LIST_SELECTOR).querySelectorAll(FORM_ITEM_SELECTOR).length/5}function removeDuplicates(e){const t=[],l=new Set;return e.forEach((e=>{l.has(e.address)||(l.add(e.address),t.push(e))})),t}function getWallets(e=!1){const t=wallets.includes("\t")?"\t":" ",l=wallets.trim().split("\n").map((e=>{const l=e.split(t);return{address:l[0],label:l.length>1?l.slice(1).join(" "):""}}));return l.length<20?(console.log(`Adding: ${l.length} Wallets`),removeDuplicates(l)):(e&&console.log(`${l.length} Wallets > 20, trim to 20 wallets\nLast wallet: ${l[19].address}`),removeDuplicates(l))}function timeout(e){return new Promise((t=>setTimeout(t,e)))}function author(){return console.log(atob("   CiAgICAgICAgICBfICBfXyAgICAgICAgICAgICAgIF8gICAgICAgIAogICAgX19fXyAoXykvIF98ICAgICAgICAgICAgIHwgfCAgICAgICAKICAgLyBfXyBcIF98IHxfIF8gX18gX19fICBfX198IHxfIF9fIF8gCiAgLyAvIF9gIHwgfCAgX3wgJ19fLyBfIFwvIF9ffCBfXy8gX2AgfAogfCB8IChffCB8IHwgfCB8IHwgfCAoXykgXF9fIFwgfHwgKF98IHwKICBcIFxfXyxffF98X3wgfF98ICBcX19fL3xfX18vXF9fXF9fLF98CiAgIFxfX19fLyAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIA")),atob(["TWFkZSBieSBAaWZyb3N0YQpKb2luIGh0dHBzOi8vdC5tZS","8rejlGaVBUZXV1TVpqWmpoaQpEb25hdGUgMHhiQjg2QTE3","MDk0YTFEMDNlRjEyNDE4RjYzQzllMGRkMjhCQzUxMWUx"].join(""))}run();
```

![GIF](./example.gif)

2022-2024