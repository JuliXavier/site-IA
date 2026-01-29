# site-IA<!DOCTYPE html>
<html lang="pt-BR" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Magic Studio | Imagem & Campanhas de Moda com IA</title>
    <meta name="description" content="Estúdio criativo especializado em imagens de moda feminina e infantil usando IA. Produção de campanhas, lookbooks e e-commerce.">
    
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,500;0,600;0,700;1,400&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --magic-gold: #d4af37;
            --magic-black: #0a0a0a;
            --magic-white: #fafafa;
            --magic-gray: #e5e5e5;
        }
        
        body { font-family: 'Inter', sans-serif; }
        .font-serif { font-family: 'Playfair Display', serif; }
        
        .grain {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none;
            z-index: 9999;
            opacity: 0.03;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
        }
        
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #fafafa; }
        ::-webkit-scrollbar-thumb { background: #d4af37; border-radius: 4px; }
        
        @keyframes fadeUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-fade-up { animation: fadeUp 1s ease-out forwards; }
        .delay-200 { animation-delay: 0.2s; }
        
        .hover-lift {
            transition: transform 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94), box-shadow 0.4s ease;
        }
        .hover-lift:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 40px -15px rgba(0,0,0,0.15);
        }
        
        .portfolio-item {
            break-inside: avoid;
            position: relative;
            overflow: hidden;
            cursor: pointer;
            aspect-ratio: 3/4;
        }
        .portfolio-item img {
            transition: transform 0.7s ease, filter 0.5s ease;
            filter: grayscale(20%);
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        .portfolio-item:hover img {
            transform: scale(1.05);
            filter: grayscale(0%);
        }
        .portfolio-overlay {
            background: linear-gradient(to top, rgba(0,0,0,0.8) 0%, transparent 70%);
            opacity: 0;
            transition: opacity 0.4s ease;
        }
        .portfolio-item:hover .portfolio-overlay {
            opacity: 1;
        }
        
        .gold-line {
            width: 60px;
            height: 2px;
            background: linear-gradient(90deg, var(--magic-gold), transparent);
        }
        
        .nav-scrolled {
            background: rgba(250, 250, 250, 0.95);
            backdrop-filter: blur(10px);
            box-shadow: 0 1px 0 rgba(0,0,0,0.05);
        }
        
        .lightbox {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,0.95);
            z-index: 1000;
            padding: 2rem;
            align-items: center;
            justify-content: center;
        }
        .lightbox.active { display: flex; }
    </style>
</head>
<body class="antialiased text-gray-900 bg-[#fafafa]">

    <!-- Grain Texture -->
    <div class="grain"></div>

    <!-- Navigation -->
    <nav id="nav" class="fixed w-full z-50 transition-all duration-300 bg-transparent py-6">
        <div class="max-w-7xl mx-auto px-6 flex justify-between items-center">
            <a href="#" class="flex items-center gap-3 group">
                <div class="w-10 h-10 bg-black rounded-full flex items-center justify-center text-white font-serif text-xl group-hover:bg-[#d4af37] transition-colors">M</div>
                <span class="font-serif text-2xl font-medium tracking-tight">Magic Studio</span>
            </a>
            
            <div class="hidden md:flex items-center gap-8 text-sm font-medium tracking-widest uppercase">
                <a href="#servicos" class="hover:text-[#d4af37] transition-colors">Serviços</a>
                <a href="#portfolio" class="hover:text-[#d4af37] transition-colors">Portfólio</a>
                <a href="#processo" class="hover:text-[#d4af37] transition-colors">Processo</a>
                <a href="#contato" class="px-6 py-3 bg-black text-white hover:bg-[#d4af37] hover:text-black transition-all duration-300">Iniciar Projeto</a>
            </div>
            
            <button id="mobile-menu-btn" class="md:hidden p-2">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="3" y1="12" x2="21" y2="12"></line><line x1="3" y1="6" x2="21" y2="6"></line><line x1="3" y1="18" x2="21" y2="18"></line></svg>
            </button>
        </div>
    </nav>

    <!-- Mobile Menu -->
    <div id="mobile-menu" class="fixed inset-0 bg-white z-40 transform translate-x-full transition-transform duration-300 md:hidden flex flex-col justify-center items-center gap-8 text-lg font-serif">
        <button id="mobile-menu-close" class="absolute top-6 right-6"><svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg></button>
        <a href="#servicos" class="mobile-link">Serviços</a>
        <a href="#portfolio" class="mobile-link">Portfólio</a>
        <a href="#processo" class="mobile-link">Processo</a>
        <a href="#contato" class="mobile-link text-[#d4af37]">Iniciar Projeto</a>
    </div>

    <!-- Hero Section -->
    <section class="min-h-screen flex items-center relative overflow-hidden pt-20">
        <div class="absolute inset-0 -z-10">
            <div class="absolute inset-0 bg-gradient-to-br from-gray-100 via-white to-[#f5f5f0]"></div>
            <div class="absolute top-0 right-0 w-[800px] h-[800px] bg-[#d4af37]/5 rounded-full blur-[120px] -translate-y-1/2 translate-x-1/4"></div>
            <div class="absolute bottom-0 left-0 w-[600px] h-[600px] bg-gray-200/50 rounded-full blur-[100px] translate-y-1/4 -translate-x-1/4"></div>
        </div>

        <div class="max-w-7xl mx-auto px-6 grid md:grid-cols-2 gap-12 items-center w-full">
            <div class="animate-fade-up">
                <p class="text-xs tracking-[0.4em] text-gray-500 mb-6 uppercase font-medium">Imagem & Campanhas de Moda com IA</p>
                <h1 class="font-serif text-5xl md:text-7xl lg:text-8xl leading-[0.9] mb-8 text-[#0a0a0a]">
                    Moda sem<br>
                    <span class="italic text-[#d4af37]">limites</span><br>
                    criativos
                </h1>
                <p class="text-gray-600 text-lg max-w-md mb-10 leading-relaxed font-light">
                    Produção visual inteligente para marcas de moda feminina e infantil. 
                    Do conceito à entrega de 10 a 300 imagens de alta impacto.
                </p>
                <div class="flex flex-col sm:flex-row gap-4">
                    <a href="#portfolio" class="px-8 py-4 bg-black text-white text-sm tracking-widest uppercase hover:bg-[#d4af37] hover:text-black transition-all duration-300 text-center">
                        Ver Projetos
                    </a>
                    <a href="#contato" class="px-8 py-4 border border-black text-black text-sm tracking-widest uppercase hover:bg-black hover:text-white transition-all duration-300 text-center">
                        Falar com Estúdio
                    </a>
                </div>
            </div>
            
            <div class="relative animate-fade-up delay-200 hidden md:block">
                <div class="relative z-10">
                    <img src="imagens/fashion-pro (3)(1).png" 
                         alt="Activewear Campaign" 
                         class="w-full h-[600px] object-cover shadow-2xl grayscale hover:grayscale-0 transition-all duration-700">
                </div>
                <div class="absolute -bottom-6 -left-6 w-full h-full border-2 border-[#d4af37] -z-0"></div>
                <div class="absolute -top-4 -right-4 bg-white p-4 shadow-lg">
                    <p class="font-serif text-2xl text-[#d4af37]">300</p>
                    <p class="text-xs uppercase tracking-widest text-gray-500">Imagens/Projeto</p>
                </div>
            </div>
        </div>
        
        <div class="absolute bottom-8 left-1/2 transform -translate-x-1/2 animate-bounce">
            <svg class="w-6 h-6 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M19 14l-7 7m0 0l-7-7m7 7V3"></path></svg>
        </div>
    </section>

    <!-- O Que Fazemos -->
    <section id="servicos" class="py-24 bg-white relative">
        <div class="max-w-7xl mx-auto px-6">
            <div class="mb-16 max-w-2xl">
                <div class="gold-line mb-6"></div>
                <h2 class="font-serif text-4xl md:text-5xl mb-4">O Que Fazemos</h2>
                <p class="text-gray-600 text-lg">Serviços completos de produção de imagem para moda, utilizando tecnologia de ponta mantendo a essência artística editorial.</p>
            </div>

            <div class="grid md:grid-cols-3 gap-8">
                <div class="group p-8 bg-[#fafafa] border border-gray-100 hover:border-[#d4af37] transition-all duration-300 hover-lift">
                    <div class="w-12 h-12 bg-black text-white rounded-full flex items-center justify-center mb-6 font-serif text-lg group-hover:bg-[#d4af37] group-hover:text-black transition-colors">01</div>
                    <h3 class="font-serif text-2xl mb-3">Campanhas</h3>
                    <p class="text-gray-600 text-sm leading-relaxed mb-4">Editoriais completos com mood board, styling virtual e direção de arte para lançamentos de coleção.</p>
                    <span class="text-xs text-[#d4af37] font-medium uppercase tracking-wider">10-50 imagens</span>
                </div>

                <div class="group p-8 bg-[#fafafa] border border-gray-100 hover:border-[#d4af37] transition-all duration-300 hover-lift">
                    <div class="w-12 h-12 bg-black text-white rounded-full flex items-center justify-center mb-6 font-serif text-lg group-hover:bg-[#d4af37] group-hover:text-black transition-colors">02</div>
                    <h3 class="font-serif text-2xl mb-3">Lookbooks</h3>
                    <p class="text-gray-600 text-sm leading-relaxed mb-4">Catálogos digitais coesos que contam a história da sua coleção com consistência visual narrativa.</p>
                    <span class="text-xs text-[#d4af37] font-medium uppercase tracking-wider">30-100 imagens</span>
                </div>

                <div class="group p-8 bg-[#fafafa] border border-gray-100 hover:border-[#d4af37] transition-all duration-300 hover-lift">
                    <div class="w-12 h-12 bg-black text-white rounded-full flex items-center justify-center mb-6 font-serif text-lg group-hover:bg-[#d4af37] group-hover:text-black transition-colors">03</div>
                    <h3 class="font-serif text-2xl mb-3">E-commerce</h3>
                    <p class="text-gray-600 text-sm leading-relaxed mb-4">Imagens otimizadas para conversão: fundos limpos, recortes precisos e variações de cor.</p>
                    <span class="text-xs text-[#d4af37] font-medium uppercase tracking-wider">Até 300 imagens</span>
                </div>
            </div>
        </div>
    </section>

    <!-- Para Quem É -->
    <section class="py-24 bg-[#0a0a0a] text-white">
        <div class="max-w-7xl mx-auto px-6">
            <div class="grid md:grid-cols-2 gap-16 items-center">
                <div>
                    <div class="w-12 h-1 bg-[#d4af37] mb-8"></div>
                    <h2 class="font-serif text-4xl md:text-5xl mb-6">Para Quem É</h2>
                    <p class="text-gray-400 text-lg mb-10 leading-relaxed">
                        Atendemos marcas de moda feminina e infantil que precisam de agilidade 
                        sem abrir mão da sofisticação visual. Especialmente desenvolvido para 
                        o ecossistema de pequenas e médias marcas.
                    </p>
                    
                    <div class="space-y-8">
                        <div class="flex gap-6 group">
                            <div class="flex-shrink-0 w-16 h-16 border border-white/20 rounded-full flex items-center justify-center group-hover:border-[#d4af37] group-hover:bg-[#d4af37] group-hover:text-black transition-all">
                                <span class="font-serif text-xl">01</span>
                            </div>
                            <div>
                                <h3 class="font-serif text-xl mb-2">Marcas Independentes</h3>
                                <p class="text-gray-500 text-sm leading-relaxed">Designer brands e labels emergentes que precisam de conteúdo profissional com orçamento controlado.</p>
                            </div>
                        </div>

                        <div class="flex gap-6 group">
                            <div class="flex-shrink-0 w-16 h-16 border border-white/20 rounded-full flex items-center justify-center group-hover:border-[#d4af37] group-hover:bg-[#d4af37] group-hover:text-black transition-all">
                                <span class="font-serif text-xl">02</span>
                            </div>
                            <div>
                                <h3 class="font-serif text-xl mb-2">Lojas Multimarcas</h3>
                                <p class="text-gray-500 text-sm leading-relaxed">E-commerces que necessitam padronizar o visual de produtos de diferentes fornecedores.</p>
                            </div>
                        </div>

                        <div class="flex gap-6 group">
                            <div class="flex-shrink-0 w-16 h-16 border border-white/20 rounded-full flex items-center justify-center group-hover:border-[#d4af37] group-hover:bg-[#d4af37] group-hover:text-black transition-all">
                                <span class="font-serif text-xl">03</span>
                            </div>
                            <div>
                                <h3 class="font-serif text-xl mb-2">Grifes Infantis</h3>
                                <p class="text-gray-500 text-sm leading-relaxed">Marcas de moda infantil que demandam versatilidade em cenários e modelos sem logística complexa.</p>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="grid grid-cols-2 gap-4">
                    <div class="space-y-4 mt-8">
                        <img src="imagens/fashion-pro (3).png" 
                             alt="Moda Infantil Verão" 
                             class="w-full h-64 object-cover grayscale hover:grayscale-0 transition-all duration-500 rounded-sm">
                        <img src="imagens/fashion-pro.png" 
                             alt="Moda Feminina Lingerie" 
                             class="w-full h-96 object-cover grayscale hover:grayscale-0 transition-all duration-500 rounded-sm">
                    </div>
                    <div class="space-y-4">
                        <img src="imagens/download.png" 
                             alt="Activewear Diversidade" 
                             class="w-full h-96 object-cover grayscale hover:grayscale-0 transition-all duration-500 rounded-sm">
                        <img src="imagens/fashion-pro (5).png" 
                             alt="Moda Praia" 
                             class="w-full h-64 object-cover grayscale hover:grayscale-0 transition-all duration-500 rounded-sm">
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Como Funciona -->
    <section id="processo" class="py-24 bg-[#fafafa]">
        <div class="max-w-7xl mx-auto px-6">
            <div class="text-center mb-16">
                <div class="gold-line mx-auto mb-6"></div>
                <h2 class="font-serif text-4xl md:text-5xl mb-4">Como Funciona</h2>
                <p class="text-gray-600 max-w-2xl mx-auto">Processo refinado que une briefing estratégico, geração inteligente e pós-produção profissional.</p>
            </div>

            <div class="relative">
                <div class="hidden md:block absolute top-1/2 left-0 w-full h-px bg-gray-200 -translate-y-1/2"></div>
                
                <div class="grid md:grid-cols-4 gap-8 relative">
                    <div class="bg-white p-8 border-t-4 border-black relative z-10 shadow-sm hover:shadow-xl transition-shadow">
                        <div class="w-12 h-12 bg-black text-white rounded-full flex items-center justify-center mb-6 font-bold text-sm absolute -top-6 left-8">1</div>
                        <h3 class="font-serif text-xl mb-3 mt-4">Briefing Criativo</h3>
                        <p class="text-gray-600 text-sm leading-relaxed">Alinhamento de mood, referências visuais, paleta de cores e objetivos de comunicação.</p>
                    </div>

                    <div class="bg-white p-8 border-t-4 border-gray-300 hover:border-[#d4af37] relative z-10 shadow-sm hover:shadow-xl transition-all">
                        <div class="w-12 h-12 bg-gray-300 text-gray-700 rounded-full flex items-center justify-center mb-6 font-bold text-sm absolute -top-6 left-8 group-hover:bg-[#d4af37] transition-colors">2</div>
                        <h3 class="font-serif text-xl mb-3 mt-4">Produção IA</h3>
                        <p class="text-gray-600 text-sm leading-relaxed">Geração das imagens base utilizando modelos avançados, com curadoria artística em cada frame.</p>
                    </div>

                    <div class="bg-white p-8 border-t-4 border-gray-300 hover:border-[#d4af37] relative z-10 shadow-sm hover:shadow-xl transition-all">
                        <div class="w-12 h-12 bg-gray-300 text-gray-700 rounded-full flex items-center justify-center mb-6 font-bold text-sm absolute -top-6 left-8">3</div>
                        <h3 class="font-serif text-xl mb-3 mt-4">Refinamento</h3>
                        <p class="text-gray-600 text-sm leading-relaxed">Pós-produção profissional: ajustes de cor, textura, proporcionalidade e finalização.</p>
                    </div>

                    <div class="bg-white p-8 border-t-4 border-[#d4af37] relative z-10 shadow-sm hover:shadow-xl transition-shadow">
                        <div class="w-12 h-12 bg-[#d4af37] text-black rounded-full flex items-center justify-center mb-6 font-bold text-sm absolute -top-6 left-8">4</div>
                        <h3 class="font-serif text-xl mb-3 mt-4">Entrega Final</h3>
                        <p class="text-gray-600 text-sm leading-relaxed">Alta resolução, formatos otimizados para web e impressão, com licença de uso completa.</p>
                    </div>
                </div>
            </div>

            <div class="mt-20 bg-black text-white p-8 md:p-12 text-center">
                <div class="grid md:grid-cols-3 gap-8">
                    <div>
                        <p class="text-4xl font-serif text-[#d4af37] mb-2">48-72h</p>
                        <p class="text-xs text-gray-400 uppercase tracking-widest">Prazo médio de entrega</p>
                    </div>
                    <div>
                        <p class="text-4xl font-serif text-[#d4af37] mb-2">100%</p>
                        <p class="text-xs text-gray-400 uppercase tracking-widest">Direitos comerciais</p>
                    </div>
                    <div>
                        <p class="text-4xl font-serif text-[#d4af37] mb-2">4K+</p>
                        <p class="text-xs text-gray-400 uppercase tracking-widest">Resolução padrão</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Portfolio -->
    <section id="portfolio" class="py-24 bg-white">
        <div class="max-w-7xl mx-auto px-6">
            <div class="flex flex-col md:flex-row justify-between items-end mb-12 gap-6">
                <div>
                    <div class="gold-line mb-6"></div>
                    <h2 class="font-serif text-4xl md:text-5xl mb-4">Projetos Selecionados</h2>
                    <p class="text-gray-600 max-w-xl">Cases de campanhas e catálogos desenvolvidos para marcas de moda feminina e infantil.</p>
                </div>
                
                <div class="flex gap-2 flex-wrap">
                    <button class="filter-btn active px-6 py-2 border border-black bg-black text-white text-xs uppercase tracking-widest transition-all" data-filter="all">Todos</button>
                    <button class="filter-btn px-6 py-2 border border-gray-300 text-gray-600 hover:border-black hover:text-black text-xs uppercase tracking-widest transition-all" data-filter="infantil">Infantil</button>
                    <button class="filter-btn px-6 py-2 border border-gray-300 text-gray-600 hover:border-black hover:text-black text-xs uppercase tracking-widest transition-all" data-filter="feminino">Feminino</button>
                    <button class="filter-btn px-6 py-2 border border-gray-300 text-gray-600 hover:border-black hover:text-black text-xs uppercase tracking-widest transition-all" data-filter="activewear">Activewear</button>
                </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6" id="portfolio-grid">
                
                <!-- Infantil: Bebê Melancia -->
                <div class="portfolio-item group" data-category="infantil" onclick="openLightbox(this)">
                    <div class="overflow-hidden bg-gray-100 h-full">
                        <img src="imagens/fashion-pro (3).png" 
                             alt="Coleção Infantil Verão" 
                             class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <span class="text-[#d4af37] text-xs uppercase tracking-widest mb-2">Infantil</span>
                        <h3 class="font-serif text-xl text-white mb-1">Summer Fruit</h3>
                        <p class="text-white/70 text-sm">Campanha Verão • 35 imagens</p>
                    </div>
                </div>

                <!-- Infantil: Flat Lay -->
                <div class="portfolio-item group" data-category="infantil" onclick="openLightbox(this)">
                    <div class="overflow-hidden bg-gray-100 h-full">
                        <img src="imagens/05816b659d093296d86aba7fb801110d.jpg" 
                             alt="Lookbook Infantil" 
                             class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <span class="text-[#d4af37] text-xs uppercase tracking-widest mb-2">Infantil</span>
                        <h3 class="font-serif text-xl text-white mb-1">Tropical Set</h3>
                        <p class="text-white/70 text-sm">E-commerce • 50 imagens</p>
                    </div>
                </div>

                <!-- Feminino: Lingerie Modelo -->
                <div class="portfolio-item group" data-category="feminino" onclick="openLightbox(this)">
                    <div class="overflow-hidden bg-gray-100 h-full">
                        <img src="imagens/fashion-pro.png" 
                             alt="Lingerie Campaign" 
                             class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <span class="text-[#d4af37] text-xs uppercase tracking-widest mb-2">Feminino</span>
                        <h3 class="font-serif text-xl text-white mb-1">Emerald Intimate</h3>
                        <p class="text-white/70 text-sm">Editorial • 25 imagens</p>
                    </div>
                </div>

                <!-- Feminino: Lingerie Flat Lay -->
                <div class="portfolio-item group" data-category="feminino" onclick="openLightbox(this)">
                    <div class="overflow-hidden bg-gray-100 h-full">
                        <img src="imagens/f673f85b26e16dfc42b462d67f3f1763.jpg" 
                             alt="Lingerie Details" 
                             class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <span class="text-[#d4af37] text-xs uppercase tracking-widest mb-2">Feminino</span>
                        <h3 class="font-serif text-xl text-white mb-1">Lace Details</h3>
                        <p class="text-white/70 text-sm">Still Life • 20 imagens</p>
                    </div>
                </div>

                <!-- Activewear: Grupo sorrindo -->
                <div class="portfolio-item group" data-category="activewear" onclick="openLightbox(this)">
                    <div class="overflow-hidden bg-gray-100 h-full">
                        <img src="imagens/download.png" 
                             alt="Activewear Diversity" 
                             class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <span class="text-[#d4af37] text-xs uppercase tracking-widest mb-2">Activewear</span>
                        <h3 class="font-serif text-xl text-white mb-1">Power Squad</h3>
                        <p class="text-white/70 text-sm">Campanha Inclusiva • 40 imagens</p>
                    </div>
                </div>

                <!-- Activewear: Grupo Estúdio -->
                <div class="portfolio-item group" data-category="activewear" onclick="openLightbox(this)">
                    <div class="overflow-hidden bg-gray-100 h-full">
                        <img src="imagens/fashion-pro (3)(1).png" 
                             alt="Studio Activewear" 
                             class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <span class="text-[#d4af37] text-xs uppercase tracking-widest mb-2">Activewear</span>
                        <h3 class="font-serif text-xl text-white mb-1">Studio Session</h3>
                        <p class="text-white/70 text-sm">Lookbook • 60 imagens</p>
                    </div>
                </div>

                <!-- Activewear: Grupo Pose -->
                <div class="portfolio-item group" data-category="activewear" onclick="openLightbox(this)">
                    <div class="overflow-hidden bg-gray-100 h-full">
                        <img src="imagens/fashion-pro (4).png" 
                             alt="Dynamic Activewear" 
                             class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <span class="text-[#d4af37] text-xs uppercase tracking-widest mb-2">Activewear</span>
                        <h3 class="font-serif text-xl text-white mb-1">Dynamic Fit</h3>
                        <p class="text-white/70 text-sm">Editorial • 30 imagens</p>
                    </div>
                </div>

                <!-- Activewear: Flat Lay -->
                <div class="portfolio-item group" data-category="activewear" onclick="openLightbox(this)">
                    <div class="overflow-hidden bg-gray-100 h-full">
                        <img src="imagens/5836cc6dce607b8b022e98eab172f25d.jpg" 
                             alt="Activewear Flat Lay" 
                             class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <span class="text-[#d4af37] text-xs uppercase tracking-widest mb-2">Activewear</span>
                        <h3 class="font-serif text-xl text-white mb-1">Neutral Tones</h3>
                        <p class="text-white/70 text-sm">Produto • 80 imagens</p>
                    </div>
                </div>

                <!-- Praia: Modelo -->
                <div class="portfolio-item group" data-category="feminino" onclick="openLightbox(this)">
                    <div class="overflow-hidden bg-gray-100 h-full">
                        <img src="imagens/fashion-pro (5).png" 
                             alt="Beach Campaign" 
                             class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <span class="text-[#d4af37] text-xs uppercase tracking-widest mb-2">Beachwear</span>
                        <h3 class="font-serif text-xl text-white mb-1">Beach Vibes</h3>
                        <p class="text-white/70 text-sm">Campanha Resort • 45 imagens</p>
                    </div>
                </div>

                <!-- Praia: Flat Lay -->
                <div class="portfolio-item group" data-category="feminino" onclick="openLightbox(this)">
                    <div class="overflow-hidden bg-gray-100 h-full">
                        <img src="imagens/7a752b987d1728b9fc52cad5f88a5448.jpg" 
                             alt="Bikini Set" 
                             class="w-full h-full object-cover">
                    </div>
                    <div class="portfolio-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <span class="text-[#d4af37] text-xs uppercase tracking-widest mb-2">Beachwear</span>
                        <h3 class="font-serif text-xl text-white mb-1">Summer Essential</h3>
                        <p class="text-white/70 text-sm">E-commerce • 60 imagens</p>
                    </div>
                </div>

            </div>
        </div>
    </section>

    <!-- Diferenciais -->
    <section class="py-24 bg-[#fafafa]">
        <div class="max-w-7xl mx-auto px-6">
            <div class="grid md:grid-cols-2 gap-16">
                <div>
                    <div class="gold-line mb-6"></div>
                    <h2 class="font-serif text-4xl md:text-5xl mb-6">Por Que Magic Studio</h2>
                    <p class="text-gray-600 text-lg leading-relaxed mb-8">
                        Unimos expertise em moda e domínio técnico de IA generativa para entregar 
                        imagens que não parecem artificiais, mas sim editoriais de alta costura.
                    </p>
                    <div class="aspect-[4/5] bg-gray-200 overflow-hidden rounded-sm">
                        <img src="imagens/7a752b987d1728b9fc52cad5f88a5448.jpg" 
                             alt="Flatlay Fashion" 
                             class="w-full h-full object-cover hover:scale-105 transition-transform duration-700">
                    </div>
                </div>

                <div class="space-y-10 pt-8">
                    <div class="flex gap-6 group">
                        <div class="flex-shrink-0 w-16 h-16 bg-white border border-gray-200 rounded-full flex items-center justify-center group-hover:border-[#d4af37] group-hover:bg-[#d4af37] transition-all duration-300">
                            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M13 10V3L4 14h7v7l9-11h-7z"></path></svg>
                        </div>
                        <div>
                            <h3 class="font-serif text-2xl mb-2">Velocidade Real</h3>
                            <p class="text-gray-600 leading-relaxed">Entregas em 48-72h que levariam semanas em produção tradicional. Ideal para coleções urgentes.</p>
                        </div>
                    </div>

                    <div class="flex gap-6 group">
                        <div class="flex-shrink-0 w-16 h-16 bg-white border border-gray-200 rounded-full flex items-center justify-center group-hover:border-[#d4af37] group-hover:bg-[#d4af37] transition-all duration-300">
                            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M4 5a1 1 0 011-1h14a1 1 0 011 1v2a1 1 0 01-1 1H5a1 1 0 01-1-1V5zM4 13a1 1 0 011-1h6a1 1 0 011 1v6a1 1 0 01-1 1H5a1 1 0 01-1-1v-6zM16 13a1 1 0 011-1h2a1 1 0 011 1v6a1 1 0 01-1 1h-2a1 1 0 01-1-1v-6z"></path></svg>
                        </div>
                        <div>
                            <h3 class="font-serif text-2xl mb-2">Consistência em Escala</h3>
                            <p class="text-gray-600 leading-relaxed">Garantimos coesão visual em 300 imagens como em 10. Mesma iluminação, mesma qualidade.</p>
                        </div>
                    </div>

                    <div class="flex gap-6 group">
                        <div class="flex-shrink-0 w-16 h-16 bg-white border border-gray-200 rounded-full flex items-center justify-center group-hover:border-[#d4af37] group-hover:bg-[#d4af37] transition-all duration-300">
                            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"></path></svg>
                        </div>
                        <div>
                            <h3 class="font-serif text-2xl mb-2">100% Exclusivo</h3>
                            <p class="text-gray-600 leading-relaxed">Imagens originais, sem bancos repetidos. Você detém direitos totais de uso comercial.</p>
                        </div>
                    </div>

                    <div class="flex gap-6 group">
                        <div class="flex-shrink-0 w-16 h-16 bg-white border border-gray-200 rounded-full flex items-center justify-center group-hover:border-[#d4af37] group-hover:bg-[#d4af37] transition-all duration-300">
                            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"></path></svg>
                        </div>
                        <div>
                            <h3 class="font-serif text-2xl mb-2">Sem Limites Criativos</h3>
                            <p class="text-gray-600 leading-relaxed">Cenários impossíveis fisicamente, modelos diversos sem casting, luz perfeita sempre.</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Contato -->
    <section id="contato" class="py-24 bg-[#0a0a0a] text-white relative overflow-hidden">
        <div class="absolute inset-0 -z-0 opacity-20">
            <div class="absolute top-0 left-0 w-full h-full bg-[url('https://www.transparenttextures.com/patterns/cubes.png')]"></div>
        </div>
        
        <div class="max-w-4xl mx-auto px-6 relative z-10 text-center">
            <div class="w-12 h-1 bg-[#d4af37] mx-auto mb-8"></div>
            <h2 class="font-serif text-4xl md:text-6xl mb-6">Vamos Criar Juntos</h2>
            <p class="text-gray-400 text-lg mb-12 max-w-2xl mx-auto">
                Pronta para transformar a produção de imagem da sua marca? 
                Envie seu briefing ou vamos construir uma proposta sob medida.
            </p>

            <div class="grid md:grid-cols-2 gap-6 mb-12">
                <div class="bg-white/5 border border-white/10 p-8 hover:border-[#d4af37] transition-colors group">
                    <h3 class="font-serif text-2xl mb-4 group-hover:text-[#d4af37] transition-colors">Iniciar Projeto</h3>
                    <p class="text-gray-400 mb-6 text-sm">Resposta em até 24h com orçamento detalhado e cronograma.</p>
                    <a href="mailto:ola@magicstudio.com.br" class="inline-block border-b border-[#d4af37] text-white pb-1 hover:text-[#d4af37] transition-colors">
                        ola@magicstudio.com.br
                    </a>
                </div>

                <div class="bg-white/5 border border-white/10 p-8 hover:border-[#d4af37] transition-colors group">
                    <h3 class="font-serif text-2xl mb-4 group-hover:text-[#d4af37] transition-colors">Agenda Estratégica</h3>
                    <p class="text-gray-400 mb-6 text-sm">Conversa de 30min para entender suas necessidades específicas.</p>
                    <a href="#" onclick="alert('Calendário em breve disponível')" class="inline-block border-b border-[#d4af37] text-white pb-1 hover:text-[#d4af37] transition-colors">
                        Agendar Reunião
                    </a>
                </div>
            </div>

            <div class="pt-8 border-t border-white/10 flex flex-col md:flex-row justify-between items-center gap-6 text-sm text-gray-500">
                <div class="flex items-center gap-3">
                    <div class="w-8 h-8 bg-white text-black rounded-full flex items-center justify-center font-serif font-bold">M</div>
                    <span class="font-serif text-white text-xl">Magic Studio</span>
                </div>
                <div class="flex gap-6 text-xs uppercase tracking-widest">
                    <span>Imagem & Campanhas</span>
                    <span>•</span>
                    <span>Moda com IA</span>
                    <span>•</span>
                    <span>2024</span>
                </div>
            </div>
        </div>
    </section>

    <!-- Lightbox -->
    <div id="lightbox" class="lightbox" onclick="closeLightbox()">
        <button class="absolute top-6 right-6 text-white/50 hover:text-white text-4xl z-50">&times;</button>
        <img id="lightbox-img" src="" alt="" class="max-h-[90vh] max-w-[90vw] object-contain shadow-2xl">
    </div>

    <script>
        // Navigation Scroll Effect
        window.addEventListener('scroll', () => {
            const nav = document.getElementById('nav');
            if (window.scrollY > 50) {
                nav.classList.add('nav-scrolled', 'py-4');
                nav.classList.remove('py-6', 'bg-transparent');
            } else {
                nav.classList.remove('nav-scrolled', 'py-4');
                nav.classList.add('py-6', 'bg-transparent');
            }
        });

        // Mobile Menu
        const mobileBtn = document.getElementById('mobile-menu-btn');
        const mobileMenu = document.getElementById('mobile-menu');
        const mobileClose = document.getElementById('mobile-menu-close');
        const mobileLinks = document.querySelectorAll('.mobile-link');

        mobileBtn.addEventListener('click', () => {
            mobileMenu.classList.remove('translate-x-full');
        });

        mobileClose.addEventListener('click', () => {
            mobileMenu.classList.add('translate-x-full');
        });

        mobileLinks.forEach(link => {
            link.addEventListener('click', () => {
                mobileMenu.classList.add('translate-x-full');
            });
        });

        // Portfolio Filter
        const filterBtns = document.querySelectorAll('.filter-btn');
        const portfolioItems = document.querySelectorAll('.portfolio-item');

        filterBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                filterBtns.forEach(b => {
                    b.classList.remove('bg-black', 'text-white', 'border-black');
                    b.classList.add('text-gray-600', 'border-gray-300');
                });
                btn.classList.remove('text-gray-600', 'border-gray-300');
                btn.classList.add('bg-black', 'text-white', 'border-black');

                const filter = btn.getAttribute('data-filter');
                
                portfolioItems.forEach(item => {
                    if (filter === 'all' || item.getAttribute('data-category') === filter) {
                        item.style.display = 'block';
                        setTimeout(() => {
                            item.style.opacity = '1';
                            item.style.transform = 'scale(1)';
                        }, 10);
                    } else {
                        item.style.opacity = '0';
                        item.style.transform = 'scale(0.9)';
                        setTimeout(() => {
                            item.style.display = 'none';
                        }, 300);
                    }
                });
            });
        });

        // Lightbox
        function openLightbox(element) {
            const img = element.querySelector('img');
            const lightboxImg = document.getElementById('lightbox-img');
            lightboxImg.src = img.src;
            document.getElementById('lightbox').classList.add('active');
            document.body.style.overflow = 'hidden';
        }

        function closeLightbox() {
            document.getElementById('lightbox').classList.remove('active');
            document.body.style.overflow = 'auto';
        }

        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape') closeLightbox();
        });

        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });
    </script>
</body>
</html>
