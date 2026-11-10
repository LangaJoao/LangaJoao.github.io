<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from 'vue'
import portrait from '../imagens/joao-langa-perfil-transparente.png'
import xitikandoLogo from '../imagens/Logo Oficial XiTikando (para perfil das redes sociais).png'
import parceriaLogo from '../imagens/Parceria360_Logo.png'
import sevenNetworksLogo from '../imagens/seven-networks-logo.png'
import ProjectGallery from './components/ProjectGallery.vue'
import nedmiRecommendation from '../imagens/carta de recomendacao/WhatsApp Image 2026-11-09 at 01.32.24.jpeg'
import mozaAward from '../imagens/Moza xLab UEM/WhatsApp Image 2026-11-09 at 01.29.54.jpeg'
import mozaParticipation from '../imagens/Moza xLab UEM/WhatsApp Image 2026-11-09 at 01.29.54 (1).jpeg'
import mobilityCertificate from '../imagens/2025 Maputo mobily Prediction Hackaton/WhatsApp Image 2026-11-09 at 01.25.41.jpeg'
const transcargaAssets = import.meta.glob('../imagens/TransCargaMoz/*.jpeg', { eager: true, query: '?url', import: 'default' })
const transcargaScreens = [
 ['01.19.57', 'Painel principal'], ['01.19.57 (1)', 'Cadastro de proprietário'],
 ['01.19.58', 'Lista de transportadores'], ['01.19.58 (1)', 'Cadastro de veículo'],
 ['01.19.58 (2)', 'Associação ao proprietário'], ['01.19.58 (3)', 'Validação de carregamentos'],
 ['01.19.59 (1)', 'Carregamento na fila FIFO'], ['01.19.59 (2)', 'Transportes realizados'],
 ['01.19.59', 'Total por veículo']
].map(([file, title]) => ({ title, src: transcargaAssets[`../imagens/TransCargaMoz/WhatsApp Image 2026-11-09 at ${file}.jpeg`] }))
import kawashLogo from '../imagens/kawash/logo.jpeg'
const xiluvaAssets = import.meta.glob('../imagens/XILUVA/*.png', { eager: true, query: '?url', import: 'default' })
const xiluvaScreens = [
 ['010813', 'Página inicial'], ['010824', 'Catálogo de presentes'], ['010835', 'Detalhe do presente'],
 ['010915', 'Painel do vendedor'], ['010926', 'Gestão de encomendas'],
 ['010939', 'Identidade da loja'], ['010955', 'Painel de administração']
].map(([file, title]) => ({ title, src: xiluvaAssets[`../imagens/XILUVA/Screenshot 2026-11-09 ${file}.png`] }))
const kawashAssets = import.meta.glob('../imagens/kawash/*.jpeg', { eager: true, query: '?url', import: 'default' })
const kawashScreens = [
 ['01.03.38 (1)', 'Identidade Kawash'], ['01.03.39 (1)', 'Escolha de perfil'],
 ['01.03.39 (2)', 'Registo de cliente'], ['01.03.39', 'Verificação do número'],
 ['01.03.36', 'Escolha de veículo'], ['01.03.37 (3)', 'Início'],
 ['01.03.38 (2)', 'Ofertas e manutenção'], ['01.03.38', 'Explorar no mapa'],
 ['01.03.39 (3)', 'Serviços de lavagem'], ['01.03.37', 'Pagamento e reserva'],
 ['01.03.38 (3)', 'Reserva enviada'], ['01.03.40', 'As minhas reservas'],
 ['01.03.40 (1)', 'Acompanhar reserva'], ['01.03.37 (1)', 'Perfil'],
 ['01.03.37 (2)', 'Kawash Explore']
].map(([file, title], index) => ({ title, src: index === 0 ? kawashLogo : kawashAssets[`../imagens/kawash/WhatsApp Image 2026-11-09 at ${file}.jpeg`] }))
const techstoreAssets = import.meta.glob('../imagens/TechStore/*.png', { eager: true, query: '?url', import: 'default' })
const techstoreScreens = [
 ['1', 'Página inicial'], ['2', 'Produtos em destaque'], ['3', 'Testemunhos'], ['4', 'Registo e rodapé'],
 ['5', 'Compra e pagamento'], ['6', 'Login'], ['7', 'Área autenticada'], ['8', 'Cadastro de produtos'],
 ['9', 'Gestão de produtos'], ['10', 'Histórico de vendas'], ['11', 'Sobre a TechStore'],
 ['12', 'Equipa'], ['13', 'Contactos'], ['14', 'Localização']
].map(([file, title]) => ({ title, src: techstoreAssets[`../imagens/TechStore/${file}.png`] }))
const waterAssets = import.meta.glob('../imagens/Abastecimento de Agua/*.png', { eager: true, query: '?url', import: 'default' })
const waterScreens = [['Menu-Abastec.png','Menu principal'],['Clie-Abastec.png','Clientes'],['Hidro-Abastec.png','Hidrômetros'],['Leit-Abastec.png','Leituras'],['Fact-Abastec.png','Faturação'],['Receb-Abast.png','Recebimentos'],['Gest-Abastec.png','Gestão interna'],['LogIn-Abastec.png','Acesso ao sistema']].map(([file,title])=>({title,src:waterAssets['../imagens/Abastecimento de Agua/'+file]}))
const cvUrl = import.meta.env.BASE_URL + 'Joao_Langa_CV_Profissional.pdf'
const menuOpen = ref(false)
const links = [{id:'projetos',title:'Projetos',subtitle:'Água, XiTikando, Mobile & IA'},{id:'sobre',title:'Sobre',subtitle:'Percurso & Tecnologias'},{id:'contacto',title:'Contacto',subtitle:'Vamos conversar'}]
const projects = [
 {name:'Seven Networks',description:'Website institucional para apresentar a empresa e os seus produtos digitais.',tags:'WEBSITE INSTITUCIONAL · PRODUTO & TECNOLOGIA',image:sevenNetworksLogo,isLogo:true,alt:'Logótipo da Seven Networks',logoClass:'seven-logo',website:'https://sevennetworks.co.mz/'},
 {name:'XiTikando',description:'Poupança em grupo, simplificada. Arquitetura, desenvolvimento full stack e deploy.',tags:'POUPANÇA EM GRUPO · FULL STACK',image:xitikandoLogo,isLogo:true,alt:'Logótipo oficial do XiTikando',website:'https://xitikando.co.mz/',app:'https://xitikando.online/'},
 {name:'Parceria360 AI',description:'Gestão de startups com aplicações web, mobile e IA conversacional.',tags:'LARAVEL · VUE · REACT NATIVE · EXPO',image:parceriaLogo,isLogo:true,alt:'Logótipo da Parceria360',logoClass:'parceria-logo'}
]
const experiences = [
 {label:'2026 — atual',org:'Parceria360',role:'Full Stack, Mobile & AI Developer'},
 {label:'Mai 2026 — atual',org:'Seven Networks',role:'Cofundador · Produto & Tecnologia',website:'https://sevennetworks.co.mz/'},
 {label:'Mar — Set 2026',org:'MozPick',role:'Especialista de TI · Testes & QA'},
 {label:'Abr 2024 — Ago 2026',org:'NEDMI · UEM',role:'Presidente · Coordenação e representação estudantil'}
]
watch(menuOpen, value => { document.body.style.overflow = value ? 'hidden' : '' })
function closeMenu(){menuOpen.value=false}
function onKey(event){if(event.key==='Escape')closeMenu()}
let revealObserver
onMounted(() => {
 window.addEventListener('keydown', onKey)
 if (window.matchMedia('(prefers-reduced-motion: reduce)').matches || !('IntersectionObserver' in window)) return
 revealObserver = new IntersectionObserver(entries => {
  entries.forEach(entry => {
   if (entry.isIntersecting) {
    entry.target.classList.add('is-visible')
    revealObserver.unobserve(entry.target)
   }
  })
 }, { threshold: 0.06 })
 document.querySelectorAll('.section-heading, .project, .about-grid > div, .credentials > div, .contact-heading, .contact-card').forEach(element => {
  element.classList.add('scroll-reveal')
  revealObserver.observe(element)
 })
})
onBeforeUnmount(()=>{revealObserver?.disconnect();document.body.style.overflow='';window.removeEventListener('keydown',onKey)})
</script>
<template>
 <header class="site-header"><nav class="container navigation" aria-label="Navegação principal"><a class="brand" href="#inicio" aria-label="João Langa — início" @click="closeMenu">JL</a><div class="desktop-links"><a href="#projetos">Projetos</a><a href="#sobre">Sobre</a><a class="button button-outline cv-button" :href="cvUrl" target="_blank" rel="noopener">Ver CV</a></div><button class="menu-toggle" :aria-expanded="menuOpen" aria-controls="mobile-menu" :aria-label="menuOpen?'Fechar menu':'Abrir menu'" @click="menuOpen=!menuOpen"><i :class="menuOpen?'pi pi-times':'pi pi-bars'" aria-hidden="true"></i></button></nav></header>
 <div v-if="menuOpen" id="mobile-menu" class="mobile-menu"><nav class="container mobile-navigation" aria-label="Navegação móvel"><a v-for="link in links" :key="link.id" :href="`#${link.id}`" @click="closeMenu"><span><strong>{{link.title}}</strong><small>{{link.subtitle}}</small></span><i class="pi pi-angle-right" aria-hidden="true"></i></a><a class="button button-outline download" :href="cvUrl" download @click="closeMenu"><i class="pi pi-download" aria-hidden="true"></i> Descarregar CV</a></nav><div class="menu-bottom"><div class="container"><p>Email de contacto</p><a class="email-link" href="mailto:joaolanga@uem.ac.mz">joaolanga@uem.ac.mz</a><div class="social-links"><a href="https://github.com/LangaJoao" target="_blank" rel="noopener">GitHub</a><a href="https://www.linkedin.com/in/jo%C3%A3o-langa-047a0b321/" target="_blank" rel="noopener">LinkedIn</a></div><div class="menu-meta"><span>© João Langa</span><span>Maputo, MZ</span></div></div></div></div>
 <main id="inicio">
 <section class="hero container"><p class="eyebrow">João Langa</p><h1>Transformo ideias em<br class="desktop-break"> produtos digitais.</h1><div class="identity"><img :src="portrait" alt="João Langa"><div><h2>Software Developer &#183; Web, Mobile & IA</h2><p>Cofundador da Seven Networks</p></div></div><div class="hero-actions"><a class="button button-primary" href="#projetos">Ver projetos </a><a class="button button-outline" href="#contacto">Vamos conversar</a></div></section>
 <section id="projetos" class="projects-section container"><div class="section-heading"><div><h2>Projetos e contribuições</h2><p class="projects-intro">Seleção de projetos com a minha participação no desenvolvimento, da conceção à implementação.</p></div><span>01 &#8212; 08</span></div><div class="project-grid">
<article class="project featured kawash-project"><div class="kawash-brand"><span class="kawash-logo"><img :src="kawashLogo" alt="Logotipo Kawash"></span><div><h3>Kawash</h3><p>Encontra. Reserva. Lava. Ganha.</p></div><span class="kawash-award">2.&#186; lugar &#183; Moza xLab &#8212; UEM</span></div><ProjectGallery portrait :screens="kawashScreens" title="Kawash"/><div class="project-title"><h3>Lavagem autom&#243;vel, na tua m&#227;o.</h3></div><p>Descoberta de servi&#231;os, escolha de viatura e acompanhamento de reservas numa aplica&#231;&#227;o mobile.</p><small>REACT NATIVE &#183; EXPO &#183; LARAVEL</small></article><article class="project featured xiluva-project"><ProjectGallery :screens="xiluvaScreens" title="Xiluva"/><div class="project-title"><h3>Xiluva</h3><i class="pi pi-gift" aria-hidden="true"></i></div><p>Marketplace de presentes que liga lojas locais a quem quer surpreender. Cat&#225;logos, encomendas, coordena&#231;&#227;o de entregas e comunica&#231;&#227;o com clientes.</p><small>MARKETPLACE &#183; PRESENTES &#183; GEST&#195;O DE LOJAS</small></article><article v-for="(project,index) in projects" :key="project.name" class="project" ><div v-if="project.image" class="project-image" :class="[{'project-logo':project.isLogo},project.logoClass]"><img :src="project.isLogo ? project.image : `https://images.unsplash.com/${project.image}?auto=format&fit=crop&w=1600&q=85`" :alt="project.alt" loading="lazy"><span v-if="!project.isLogo" class="private-label">Projeto privado</span></div><div v-else class="project-concept"><strong>{{project.mark}}</strong><span>{{project.caption}}</span></div><div class="project-title"><h3>{{project.name}}</h3></div><p>{{project.description}}</p><small>{{project.tags}}</small><div v-if="project.website" class="project-links"><a :href="project.website" target="_blank" rel="noopener">Visitar website</a><a v-if="project.app" :href="project.app" target="_blank" rel="noopener">Abrir aplica&#231;&#227;o</a></div></article>
<article class="project featured water-project">
 <ProjectGallery button-mode :screens="waterScreens" title="Sistema de Abastecimento de &#193;gua"/><div class="project-title"><h3>Sistema de Abastecimento de Água</h3><i class="pi pi-tint" aria-hidden="true"></i></div><p>Aplicação desktop inteiramente desenvolvida em Java, com interface Swing, para gerir clientes, leituras, faturação e recebimentos.</p><small>JAVA · SWING · APLICAÇÃO DESKTOP</small>
</article>
<article class="project featured techstore-project"><ProjectGallery button-mode :screens="techstoreScreens" title="TechStore"/><div class="project-title"><h3>TechStore</h3><i class="pi pi-shopping-bag" aria-hidden="true"></i></div><p>Loja online de equipamentos eletr&#243;nicos, desenvolvida em equipa, com navega&#231;&#227;o responsiva e pagamentos por M-Pesa, E-Mola e cart&#227;o banc&#225;rio.</p><small>JAVA &#183; BACKEND | REACT &#183; FRONTEND | MYSQL &#183; BASE DE DADOS</small></article>


<article class="project featured transcarga-project"><ProjectGallery button-mode :screens="transcargaScreens" title="TransCargaMo&#231;ambique"/><div class="project-title"><h3>TransCargaMo&#231;ambique</h3><i class="pi pi-truck" aria-hidden="true"></i></div><p>Projeto acad&#233;mico de Estruturas de Dados em Java: listas ligadas e filas FIFO aplicadas &#224; gest&#227;o de ve&#237;culos, propriet&#225;rios e carregamentos.</p><small>JAVA &#183; LISTAS LIGADAS &#183; FILAS FIFO &#183; REPOSIT&#211;RIO P&#218;BLICO</small><div class="project-links"><a href="https://github.com/LangaJoao/TransCargaMocambique" target="_blank" rel="noopener"><i class="pi pi-github" aria-hidden="true"></i> Ver c&#243;digo no GitHub</a></div></article>
</div></section>
 <section id="sobre" class="about-section"><div class="container about-grid"><div><p class="eyebrow">Sobre</p><h2>Transformo ideias em produtos digitais. Combino desenvolvimento web e mobile, integração de IA e qualidade de software com visão de produto e liderança colaborativa.</h2><div class="technologies"><span v-for="tech in ['Laravel','Vue.js','React Native','Expo','Java','MySQL','APIs de IA','Git / Linux','Testes & QA']" :key="tech">{{tech}}</span></div></div><div class="experience"><p class="eyebrow">Percurso</p><article v-for="experience in experiences" :key="experience.org"><span>{{experience.label}}</span><div><h3><a v-if="experience.website" :href="experience.website" target="_blank" rel="noopener">{{experience.org}}</a><template v-else>{{experience.org}}</template></h3><p>{{experience.role}}</p><a v-if="experience.org==='NEDMI · UEM'" class="recommendation-card" :href="nedmiRecommendation" target="_blank" rel="noopener"><img :src="nedmiRecommendation" alt="Carta de recomenda&#231;&#227;o da Chefe do Departamento de Matem&#225;tica e Inform&#225;tica da UEM" loading="lazy"><span><strong>Carta de recomenda&#231;&#227;o</strong><small>Prof.&#170; Doutora Iara Cristina Alvarinho Gon&#231;alves &#183; Chefe do DMI</small><small>25 de novembro de 2025</small><em>Abrir carta</em></span></a></div></article><p class="location"><i class="pi pi-map-marker" aria-hidden="true"></i> Maputo, Moçambique</p></div></div></section>
 <section class="credentials container"><div><p class="eyebrow">Forma&#231;&#227;o</p><h3>Licenciatura em Inform&#225;tica</h3><p>Universidade Eduardo Mondlane &#183; 2023 &#8212; atual</p><p>Governo Eletr&#243;nico &#183; State University of Geological Research &#183; Dez 2025</p><p>Alibaba Cloud Academy &#183; MySQL e Cloud Computing &#183; Ago 2025</p></div><div><p class="eyebrow">Conquistas</p><h3>2.&#186; lugar &#183; Moza xLab &#8212; UEM</h3><p>Kawash &#183; 1.&#170; edi&#231;&#227;o do Hackathon &#183; 22 e 23 de outubro de 2026</p><div class="moza-certificates"><a class="certificate-card" :href="mozaAward" target="_blank" rel="noopener"><img :src="mozaAward" alt="Certificado de segundo lugar de Jo&#227;o Langa no Hackathon Moza xLab UEM" loading="lazy"><span>Certificado de 2.&#186; lugar</span></a><a class="certificate-card" :href="mozaParticipation" target="_blank" rel="noopener"><img :src="mozaParticipation" alt="Certificados de participa&#231;&#227;o e segundo lugar no Hackathon Moza xLab UEM" loading="lazy"><span>Certificado de participa&#231;&#227;o</span></a></div><h3>4.&#186; lugar entre 30 equipas &#183; Zindi</h3><p>2025 Maputo Mobility Prediction Hackathon &#183; 11 de outubro de 2025</p><p>Previs&#227;o de tempos de viagem de t&#225;xi em Maputo com dados meteorol&#243;gicos e de trajetos.</p><a class="certificate-card" :href="mobilityCertificate" target="_blank" rel="noopener" aria-label="Abrir certificado do Maputo Mobility Prediction Hackathon"><img :src="mobilityCertificate" alt="Certificado Zindi: 4.&#186; lugar entre 30 equipas no Maputo Mobility Prediction Hackathon de 2025" loading="lazy"><span>Ver certificado</span></a><p>Portugu&#234;s nativo &#183; Ingl&#234;s interm&#233;dio &#183; Changana fluente</p></div></section><section id="contacto" class="contact-section container"><div class="contact-heading"><span class="accent-line"></span><h2>Vamos construir o<br> próximo projeto.</h2><p>Disponível para novos desafios e colaborações técnicas.</p></div><div class="contact-card"><span class="at-symbol" aria-hidden="true">@</span><a class="button button-primary" href="mailto:joaolanga@uem.ac.mz"><i class="pi pi-send" aria-hidden="true"></i> Enviar email</a><a class="email-link" href="mailto:joaolanga@uem.ac.mz">joaolanga@uem.ac.mz</a><div class="phone-links"><a href="tel:+258868728470">+258 86 872 8470</a><a href="tel:+258833740825">+258 83 374 0825</a></div></div><div class="contact-details"><div class="social-links"><a href="https://github.com/LangaJoao" target="_blank" rel="noopener"><i class="pi pi-github" aria-hidden="true"></i> GitHub</a><a href="https://www.linkedin.com/in/jo%C3%A3o-langa-047a0b321/" target="_blank" rel="noopener"><i class="pi pi-linkedin" aria-hidden="true"></i> LinkedIn</a></div><p><i class="pi pi-map-marker" aria-hidden="true"></i> Maputo, Moçambique</p></div></section>
 </main>
<footer><div class="container footer-content"><span>© {{new Date().getFullYear()}} João Langa</span><a href="#inicio" aria-label="Voltar ao topo">↑</a></div></footer>
</template>
