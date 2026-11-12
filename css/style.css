const books = [
 {id:"b1",title:"The Alchemist",author:"Paulo Coelho",genre:"Fiction",year:1988,cover:"#e9d7b2",description:"A young shepherd travels in search of a treasure and discovers lessons about purpose, courage and listening to his heart.",rating:4.7,new:false},
 {id:"b2",title:"Wings of Fire",author:"A. P. J. Abdul Kalam",genre:"Biography",year:1999,cover:"#d5e3ef",description:"An inspiring autobiography about learning, perseverance, science and public service.",rating:4.8,new:true},
 {id:"b3",title:"A Brief History of Time",author:"Stephen Hawking",genre:"Science",year:1988,cover:"#d8d5ee",description:"An accessible introduction to big questions about the universe, space and time.",rating:4.5,new:false},
 {id:"b4",title:"Clean Code",author:"Robert C. Martin",genre:"Technology",year:2008,cover:"#d5e9dc",description:"A practical guide to writing code that is clear, understandable and easier to maintain.",rating:4.6,new:true},
 {id:"b5",title:"The Discovery of India",author:"Jawaharlal Nehru",genre:"History",year:1946,cover:"#efd8d1",description:"A wide-ranging exploration of India's history, culture and intellectual traditions.",rating:4.3,new:false},
 {id:"b6",title:"Atomic Habits",author:"James Clear",genre:"Self-help",year:2018,cover:"#f1e5b9",description:"A practical look at how small habits and consistent systems can support meaningful change.",rating:4.7,new:true},
 {id:"b7",title:"The Hobbit",author:"J. R. R. Tolkien",genre:"Fiction",year:1937,cover:"#dce8c8",description:"A fantasy adventure that follows Bilbo Baggins on an unexpected journey.",rating:4.8,new:false},
 {id:"b8",title:"The Code Book",author:"Simon Singh",genre:"Science",year:1999,cover:"#e8d9ed",description:"A history of codes and codebreaking, from ancient ciphers to modern cryptography.",rating:4.4,new:true}
];
const $ = s => document.querySelector(s);
const page = document.body.dataset.page;
const navItems = [["index.html","Home","home"],["catalogue.html","Catalogue","catalogue"],["new-arrivals.html","New Arrivals","arrivals"],["issue-book.html","Issue a Book","issue"],["my-books.html","My Books","mybooks"],["contact.html","Contact","contact"]];
function setupLayout(){
 const header=$("#siteHeader"), footer=$("#siteFooter");
 if(header) header.innerHTML=`<header class="site-header"><div class="nav-wrap"><a class="brand" href="index.html">PageTurn<span>.</span></a><button class="menu-toggle" id="menuToggle" aria-label="Toggle navigation" aria-expanded="false">☰ Menu</button><nav class="nav-links" id="navLinks">${navItems.map(([url,label,key])=>`<a class="${page===key?'active':''}" href="${url}">${label}</a>`).join("")}</nav></div></header>`;
 if(footer) footer.innerHTML=`<footer class="site-footer"><div class="footer-inner"><p>© ${new Date().getFullYear()} PageTurn Library · Student Web Development Project</p><p>Made with HTML, CSS & JavaScript</p></div></footer>`;
 const toggle=$("#menuToggle"), links=$("#navLinks");
 if(toggle) toggle.addEventListener("click",()=>{const open=links.classList.toggle("open");toggle.setAttribute("aria-expanded",String(open));});
}
function bookCard(b){return `<article class="book-card"><div class="book-cover" style="--cover:${b.cover}">${b.title}</div><span class="tag">${b.genre}</span><h3>${b.title}</h3><p class="author">by ${b.author}</p><div class="card-actions"><a class="btn btn-outline" href="book-details.html?id=${b.id}">Details</a><a class="btn" href="issue-book.html?book=${b.id}">Borrow</a></div></article>`;}
function renderHome(){const el=$("#featuredBooks");if(el)el.innerHTML=books.slice(0,4).map(bookCard).join("");}
function renderCatalogue(){
 const grid=$("#catalogueBooks"), search=$("#bookSearch"), filter=$("#genreFilter");if(!grid)return;
 const draw=()=>{const q=search.value.trim().toLowerCase(),g=filter.value;const found=books.filter(b=>(g==="all"||b.genre===g)&&(`${b.title} ${b.author}`.toLowerCase().includes(q)));grid.innerHTML=found.length?found.map(bookCard).join(""):`<div class="empty-state">No books match your search. Try another title or genre.</div>`;$("#catalogueCount").textContent=`Showing ${found.length} of ${books.length} books`;};
 search.addEventListener("input",draw);filter.addEventListener("change",draw);draw();
}
function renderDetails(){
 const el=$("#bookDetails");if(!el)return;const id=new URLSearchParams(location.search).get("id")||"b1";const b=books.find(x=>x.id===id)||books[0];
 el.innerHTML=`<div class="detail-cover" style="background:${b.cover}">${b.title}</div><div><span class="tag">${b.genre}</span><h2>${b.title}</h2><p class="muted">By ${b.author} · Published ${b.year}</p><p>${b.description}</p><p><strong>Reader rating:</strong> ★ ${b.rating}/5</p><p><strong>Availability:</strong> Available in this demo catalogue</p><a class="btn" href="issue-book.html?book=${b.id}">Issue this book</a></div>`;
}
function getIssued(){try{return JSON.parse(localStorage.getItem("pageturnIssued")||"[]");}catch{return [];}}
function saveIssued(items){localStorage.setItem("pageturnIssued",JSON.stringify(items));}
function setupIssue(){
 const form=$("#issueForm");if(!form)return;const select=$("#issueBookSelect");
 select.innerHTML='<option value="">Choose a book</option>'+books.map(b=>`<option value="${b.id}">${b.title} — ${b.author}</option>`).join("");
 const today=new Date();const iso=d=>{const x=new Date(d.getTime()-d.getTimezoneOffset()*60000);return x.toISOString().slice(0,10);};
 $("#issueDate").value=iso(today);const due=new Date(today);due.setDate(due.getDate()+7);$("#dueDate").value=iso(due);select.value=new URLSearchParams(location.search).get("book")||"";
 form.addEventListener("submit",e=>{e.preventDefault();if(!form.reportValidity())return;const data=new FormData(form),book=books.find(b=>b.id===data.get("bookId"));if(!book)return;const issueDate=data.get("issueDate"),dueDate=data.get("dueDate");if(dueDate<issueDate){$("#issueMessage").textContent="Due date cannot be before the issue date.";return;}const list=getIssued();list.push({recordId:Date.now(),studentName:data.get("studentName"),studentId:data.get("studentId"),bookId:book.id,title:book.title,author:book.author,issueDate,dueDate});saveIssued(list);form.reset();$("#issueMessage").textContent=`“${book.title}” has been added to My Books on this device.`;});
}
function renderMyBooks(){
 const el=$("#myBooksList");if(!el)return;const list=getIssued();el.innerHTML=list.length?list.slice().reverse().map(item=>`<article class="issued-item"><div><h3>${item.title}</h3><p>By ${item.author} · Issued to ${escapeHtml(item.studentName)} (${escapeHtml(item.studentId)})</p><p>Issue date: ${item.issueDate} · Due date: ${item.dueDate}</p></div><span class="tag">Demo record</span></article>`).join(""):`<div class="empty-state">You haven't issued any books yet.<br><a class="text-link" href="catalogue.html">Browse the catalogue →</a></div>`;
 const clear=$("#clearBooks");if(clear)clear.addEventListener("click",()=>{if(confirm("Clear all demo issue records saved on this device?")){saveIssued([]);renderMyBooks();}});
}
function escapeHtml(s){return String(s).replace(/[&<>"']/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]));}
function renderArrivals(){const el=$("#newArrivals");if(el)el.innerHTML=books.filter(b=>b.new).map(bookCard).join("");}
function setupContact(){const form=$("#contactForm");if(!form)return;form.addEventListener("submit",e=>{e.preventDefault();if(form.reportValidity()){$("#contactMessage").textContent="Thanks! Your demo message has been recorded on this page. No email was sent.";form.reset();}});}
document.addEventListener("DOMContentLoaded",()=>{setupLayout();renderHome();renderCatalogue();renderDetails();setupIssue();renderMyBooks();renderArrivals();setupContact();});
