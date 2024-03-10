checkboxes.forEach((checkbox) => {
// В данном случае надо использовать change, т.к. click по label вызывает клик по чекбоксу
checkbox.addEventListener("change", (event) => {
if (event.target.checked === false) {
code.innerHTML = "";
return;
}
code.innerHTML += linux_cmd[event.target.name];
});
});

https://www.freecodecamp.org/news/node-version-manager-nvm-install-guide/
https://upstackhq.com/blog/software-development/how-to-install-node-js-on-linux
