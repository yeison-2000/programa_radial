<template>
    <div class="inicio-page">
        <!-- Hero Section Principal -->
        <section class="hero-main">
            <div class="hero-background">
                <div class="sound-waves">
                    <div class="wave wave-1"></div>
                    <div class="wave wave-2"></div>
                    <div class="wave wave-3"></div>
                    <div class="wave wave-4"></div>
                    <div class="wave wave-5"></div>
                </div>
                <div class="floating-elements">
                    <div class="float-element element-1">
                        <v-icon size="30" color="white">mdi-radio</v-icon>
                    </div>
                    <div class="float-element element-2">
                        <v-icon size="25" color="white">mdi-microphone</v-icon>
                    </div>
                    <div class="float-element element-3">
                        <v-icon size="35" color="white">mdi-music-note</v-icon>
                    </div>
                    <div class="float-element element-4">
                        <v-icon size="28" color="white">mdi-broadcast</v-icon>
                    </div>
                    <div class="float-element element-5">
                        <v-icon size="32" color="white">mdi-radio-tower</v-icon>
                    </div>
                    <div class="float-element element-6">♪</div>
                    <div class="float-element element-7">♫</div>
                    <div class="float-element element-8">♪</div>
                </div>
            </div>

            <v-container>
                <div class="hero-content">
                    <h1 class="hero-title">
                        <span class="title-main">Radio Escolar</span>
                        <span class="title-highlight">Santa María Goretti</span>
                    </h1>

                    <p class="hero-subtitle">
                        La voz de nuestra comunidad educativa
                    </p>

                    <p class="hero-description">
                        Bienvenidos a nuestro espacio radiofónico, donde las voces estudiantiles
                        cobran vida y la creatividad no tiene límites. Somos más que una radio
                        escolar, somos el latido de nuestra institución.
                    </p>

                    <div class="hero-actions">
                        <v-btn size="x-large" color="white" variant="elevated" class="main-btn" @click="scrollToAbout">
                            <v-icon start size="large">mdi-play-circle</v-icon>
                            Descubre Más
                        </v-btn>

                        <v-btn size="x-large" variant="outlined" color="white" class="secondary-btn"
                            :to="'/programas'">>
                            <v-icon start>mdi-playlist-play</v-icon>
                            Nuestros Programas
                        </v-btn>
                    </div>

                    <div class="hero-stats">
                        <div class="stat-card">
                            <div class="stat-number">{{ currentYear - 2020 }}+</div>
                            <div class="stat-label">Años al Aire</div>
                            <v-icon color="white" size="small">mdi-calendar-check</v-icon>
                        </div>
                        <div class="stat-card">
                            <div class="stat-number">50+</div>
                            <div class="stat-label">Estudiantes</div>
                            <v-icon color="white" size="small">mdi-account-group</v-icon>
                        </div>
                        <div class="stat-card">
                            <div class="stat-number">500+</div>
                            <div class="stat-label">Oyentes</div>
                            <v-icon color="white" size="small">mdi-headphones</v-icon>
                        </div>
                    </div>
                </div>
            </v-container>
        </section>

        <!-- About Section -->
        <section class="about-section" ref="aboutSection">
            <v-container>
                <div class="about-content">
                    <div class="about-text">
                        <div class="section-badge">
                            <v-icon color="green">mdi-school</v-icon>
                            <span>NUESTRA HISTORIA</span>
                        </div>

                        <h2 class="about-title">
                            Más que una Radio,
                            <span class="title-accent">una Experiencia</span>
                        </h2>

                        <div class="about-description">
                            <p>
                                En el Colegio Santa María Goretti creemos que cada estudiante tiene una voz única
                                que merece ser escuchada. Nuestra radio escolar nació como un proyecto
                                educativo innovador que busca desarrollar las habilidades comunicativas,
                                la creatividad y el liderazgo de nuestros jóvenes.
                            </p>

                            <p>
                                A través de nuestros programas, los estudiantes no solo aprenden sobre
                                comunicación y medios, sino que también exploran temas académicos,
                                culturales y sociales de una manera dinámica y entretenida.
                            </p>
                        </div>

                        <div class="mission-values">
                            <div class="value-item">
                                <div class="value-icon">
                                    <v-icon size="40" color="green">mdi-lightbulb</v-icon>
                                </div>
                                <div class="value-content">
                                    <h4>Creatividad</h4>
                                    <p>Fomentamos la expresión creativa en cada programa</p>
                                </div>
                            </div>

                            <div class="value-item">
                                <div class="value-icon">
                                    <v-icon size="40" color="blue">mdi-account-multiple</v-icon>
                                </div>
                                <div class="value-content">
                                    <h4>Comunidad</h4>
                                    <p>Conectamos a toda la familia educativa</p>
                                </div>
                            </div>

                            <div class="value-item">
                                <div class="value-icon">
                                    <v-icon size="40" color="orange">mdi-star</v-icon>
                                </div>
                                <div class="value-content">
                                    <h4>Excelencia</h4>
                                    <p>Buscamos la calidad en cada producción</p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="about-visual">
                        <div class="visual-container">
                            <div class="main-circle">
                                <v-icon size="80" color="white">mdi-radio</v-icon>
                            </div>
                            <div class="orbit-circle orbit-1">
                                <v-icon size="30" color="green">mdi-microphone</v-icon>
                            </div>
                            <div class="orbit-circle orbit-2">
                                <v-icon size="30" color="blue">mdi-music-note</v-icon>
                            </div>
                            <div class="orbit-circle orbit-3">
                                <v-icon size="30" color="orange">mdi-broadcast</v-icon>
                            </div>
                            <div class="orbit-circle orbit-4">
                                <v-icon size="30" color="purple">mdi-headphones</v-icon>
                            </div>
                        </div>
                    </div>
                </div>
            </v-container>
        </section>

        <!-- Features Section -->
        <section class="features-section">
            <div class="features-background">
                <div class="bg-pattern"></div>
            </div>

            <v-container>
                <div class="section-header">
                    <div class="section-badge light">
                        <v-icon color="green">mdi-star-circle</v-icon>
                        <span>CARACTERÍSTICAS</span>
                    </div>
                    <h2 class="section-title">¿Qué nos hace especiales?</h2>
                    <p class="section-description">
                        Descubre las características que hacen única a nuestra radio escolar
                    </p>
                </div>

                <div class="features-grid">
                    <div class="feature-card" v-for="(feature, index) in features" :key="index">
                        <div class="feature-icon" :style="{ background: feature.gradient }">
                            <v-icon size="x-large" color="white">{{ feature.icon }}</v-icon>
                        </div>
                        <div class="feature-content">
                            <h3 class="feature-title">{{ feature.title }}</h3>
                            <p class="feature-description">{{ feature.description }}</p>
                        </div>
                        <div class="feature-hover-effect"></div>
                    </div>
                </div>
            </v-container>
        </section>

        <!-- CTA Section -->
        <section class="cta-section">
            <v-container>
                <div class="cta-content">
                    <div class="cta-icon">
                        <v-icon size="60" color="white">mdi-radio-tower</v-icon>
                    </div>

                    <h2 class="cta-title">¿Listo para Escucharnos?</h2>
                    <p class="cta-description">
                        Únete a nuestra comunidad de oyentes y descubre el talento
                        de los estudiantes del Colegio María Goretti
                    </p>

                    <div class="cta-actions">
                        <v-btn size="x-large" color="white" variant="elevated" class="cta-btn primary"
                            :to="'/programas'">
                            <v-icon start size="large">mdi-play</v-icon>
                            Explorar Programas
                        </v-btn>

                        <v-btn size="x-large" variant="outlined" color="white" class="cta-btn secondary"
                            :to="'/creditos'">
                            <v-icon start>mdi-account-group</v-icon>
                            Conocer el Equipo
                        </v-btn>
                    </div>

                </div>
            </v-container>
        </section>
    </div>
</template>

<script>
export default {
    name: "InicioPage",

    data() {
        return {
            currentYear: new Date().getFullYear(),

            features: [
                {
                    icon: "mdi-account-voice",
                    title: "Producción Estudiantil",
                    description: "Cada programa es creado íntegramente por nuestros estudiantes, desde la investigación hasta la edición final.",
                    gradient: "linear-gradient(135deg, #667eea 0%, #764ba2 100%)"
                },
                {
                    icon: "mdi-microphone-variant",
                    title: "Calidad Profesional",
                    description: "Utilizamos equipos de grabación profesional y técnicas avanzadas de producción radiofónica.",
                    gradient: "linear-gradient(135deg, #f093fb 0%, #f5576c 100%)"
                },
                {
                    icon: "mdi-school-outline",
                    title: "Enfoque Educativo",
                    description: "Cada programa tiene un propósito pedagógico que complementa el aprendizaje en el aula.",
                    gradient: "linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)"
                },
                {
                    icon: "mdi-heart",
                    title: "Contenido Original",
                    description: "Desarrollamos contenido único que refleja los intereses y talentos de nuestra comunidad.",
                    gradient: "linear-gradient(135deg, #43e97b 0%, #38f9d7 100%)"
                },
                {
                    icon: "mdi-broadcast",
                    title: "Alcance Comunitario",
                    description: "Nuestros programas llegan a toda la comunidad educativa y sus familias.",
                    gradient: "linear-gradient(135deg, #fa709a 0%, #fee140 100%)"
                },
                {
                    icon: "mdi-trophy",
                    title: "Reconocimiento",
                    description: "Hemos sido reconocidos por la calidad e innovación de nuestras producciones radiofónicas.",
                    gradient: "linear-gradient(135deg, #a8edea 0%, #fed6e3 100%)"
                }
            ]
        };
    },

    methods: {
        scrollToAbout() {
            this.$refs.aboutSection.scrollIntoView({
                behavior: 'smooth',
                block: 'start'
            });
        },

        goToPrograms() {
            // Navegación a la página de programas
            console.log('Navegando al equipo...');
        },

        goToTeam() {
            // Navegación a la página del equipo
            console.log('Navegando al equipo...');
        }
    }
};
</script>

<style scoped>
.inicio-page {
    min-height: 100vh;
    background: #ffffff;
    overflow-x: hidden;
}

/* Hero Section Principal */
.hero-main {
    position: relative;
    min-height: 100vh;
    background: linear-gradient(135deg, #1b5e20 0%, #2e7d32 30%, #388e3c 70%, #4caf50 100%);
    color: white;
    display: flex;
    align-items: center;
    overflow: hidden;
}

.hero-background {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    overflow: hidden;
}

.sound-waves {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

.wave {
    position: absolute;
    border: 2px solid rgba(255, 255, 255, 0.1);
    border-radius: 50%;
    animation: wave-expand 4s ease-in-out infinite;
}

.wave-1 {
    width: 100px;
    height: 100px;
    top: -50px;
    left: -50px;
    animation-delay: 0s;
}

.wave-2 {
    width: 200px;
    height: 200px;
    top: -100px;
    left: -100px;
    animation-delay: 0.8s;
}

.wave-3 {
    width: 300px;
    height: 300px;
    top: -150px;
    left: -150px;
    animation-delay: 1.6s;
}

.wave-4 {
    width: 400px;
    height: 400px;
    top: -200px;
    left: -200px;
    animation-delay: 2.4s;
}

.wave-5 {
    width: 500px;
    height: 500px;
    top: -250px;
    left: -250px;
    animation-delay: 3.2s;
}

@keyframes wave-expand {
    0% {
        transform: scale(0.8);
        opacity: 0;
    }

    50% {
        opacity: 0.6;
    }

    100% {
        transform: scale(1.2);
        opacity: 0;
    }
}

.floating-elements {
    position: absolute;
    width: 100%;
    height: 100%;
    pointer-events: none;
}

.float-element {
    position: absolute;
    animation: float-around 8s ease-in-out infinite;
    opacity: 0.3;
}

.element-1 {
    top: 10%;
    left: 10%;
    animation-delay: 0s;
}

.element-2 {
    top: 20%;
    right: 15%;
    animation-delay: 1s;
}

.element-3 {
    top: 60%;
    left: 5%;
    animation-delay: 2s;
}

.element-4 {
    bottom: 30%;
    right: 20%;
    animation-delay: 3s;
}

.element-5 {
    bottom: 10%;
    left: 30%;
    animation-delay: 4s;
}

.element-6 {
    top: 40%;
    right: 10%;
    font-size: 2rem;
    animation-delay: 5s;
}

.element-7 {
    top: 70%;
    left: 70%;
    font-size: 1.5rem;
    animation-delay: 6s;
}

.element-8 {
    top: 30%;
    left: 60%;
    font-size: 2rem;
    animation-delay: 7s;
}

@keyframes float-around {

    0%,
    100% {
        transform: translateY(0px) rotate(0deg);
    }

    25% {
        transform: translateY(-15px) rotate(90deg);
    }

    50% {
        transform: translateY(-30px) rotate(180deg);
    }

    75% {
        transform: translateY(-15px) rotate(270deg);
    }
}

.hero-content {
    position: relative;
    z-index: 2;
    text-align: center;
    max-width: 900px;
    margin: 0 auto;
    padding: 40px 20px;
}

.hero-badge {
    display: inline-flex;
    align-items: center;
    gap: 12px;
    background: rgba(255, 255, 255, 0.1);
    padding: 12px 24px;
    border-radius: 30px;
    margin-bottom: 30px;
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
    position: relative;
    overflow: hidden;
}

.badge-pulse {
    position: absolute;
    left: 8px;
    top: 50%;
    transform: translateY(-50%);
    width: 12px;
    height: 12px;
    background: #ff5252;
    border-radius: 50%;
    animation: pulse-dot 2s ease-in-out infinite;
}

@keyframes pulse-dot {

    0%,
    100% {
        transform: translateY(-50%) scale(1);
        opacity: 1;
    }

    50% {
        transform: translateY(-50%) scale(1.3);
        opacity: 0.7;
    }
}

.radio-icon {
    animation: radio-pulse 3s ease-in-out infinite;
}

@keyframes radio-pulse {

    0%,
    100% {
        transform: scale(1);
    }

    50% {
        transform: scale(1.1);
    }
}

.hero-title {
    margin-bottom: 20px;
    line-height: 1.1;
}

.title-main {
    display: block;
    font-size: 2.8rem;
    font-weight: 300;
    opacity: 0.9;
    margin-bottom: 10px;
}

.title-highlight {
    display: block;
    font-size: 4rem;
    font-weight: 800;
    background: linear-gradient(45deg, #81c784, #a5d6a7, #c8e6c9);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    text-shadow: none;
}

.hero-subtitle {
    font-size: 1.4rem;
    font-weight: 400;
    margin-bottom: 25px;
    opacity: 0.9;
    font-style: italic;
}

.hero-description {
    font-size: 1.2rem;
    line-height: 1.7;
    margin-bottom: 40px;
    opacity: 0.9;
    max-width: 700px;
    margin-left: auto;
    margin-right: auto;
}

.hero-actions {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin-bottom: 60px;
    flex-wrap: wrap;
}

.main-btn,
.secondary-btn {
    padding: 18px 35px !important;
    font-size: 1.1rem !important;
    font-weight: 600 !important;
    border-radius: 35px !important;
    transition: all 0.3s ease !important;
    min-width: 200px;
}

.main-btn:hover {
    transform: translateY(-3px);
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.secondary-btn:hover {
    transform: translateY(-3px);
    background: rgba(255, 255, 255, 0.1);
}

.hero-stats {
    display: flex;
    justify-content: center;
    gap: 40px;
    flex-wrap: wrap;
}

.stat-card {
    text-align: center;
    background: rgba(255, 255, 255, 0.1);
    padding: 25px 20px;
    border-radius: 15px;
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
    transition: all 0.3s ease;
    min-width: 140px;
}

.stat-card:hover {
    transform: translateY(-5px);
    background: rgba(255, 255, 255, 0.15);
}

.stat-number {
    font-size: 2.2rem;
    font-weight: 700;
    color: #81c784;
    margin-bottom: 8px;
}

.stat-label {
    font-size: 0.9rem;
    opacity: 0.9;
    text-transform: uppercase;
    letter-spacing: 1px;
    margin-bottom: 8px;
}

/* About Section */
.about-section {
    padding: 100px 0;
    background: #f8f9fa;
}

.about-content {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: center;
}

.section-badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: rgba(46, 125, 50, 0.1);
    color: #2e7d32;
    padding: 8px 16px;
    border-radius: 20px;
    font-size: 0.9rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 1px;
    margin-bottom: 25px;
}

.section-badge.light {
    background: rgba(255, 255, 255, 0.2);
    color: white;
}

.about-title {
    font-size: 2.8rem;
    font-weight: 700;
    color: #1b5e20;
    margin-bottom: 30px;
    line-height: 1.2;
}

.title-accent {
    background: linear-gradient(45deg, #2e7d32, #4caf50);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

.about-description {
    margin-bottom: 40px;
}

.about-description p {
    font-size: 1.1rem;
    line-height: 1.8;
    color: #555;
    margin-bottom: 20px;
}

.mission-values {
    display: flex;
    flex-direction: column;
    gap: 30px;
}

.value-item {
    display: flex;
    align-items: flex-start;
    gap: 20px;
    padding: 25px;
    background: white;
    border-radius: 15px;
    box-shadow: 0 5px 20px rgba(0, 0, 0, 0.08);
    transition: all 0.3s ease;
}

.value-item:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 40px rgba(0, 0, 0, 0.12);
}

.value-icon {
    flex-shrink: 0;
    width: 70px;
    height: 70px;
    background: rgba(46, 125, 50, 0.1);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
}

.value-content h4 {
    font-size: 1.3rem;
    font-weight: 600;
    color: #1b5e20;
    margin-bottom: 8px;
}

.value-content p {
    color: #666;
    line-height: 1.6;
}

.about-visual {
    display: flex;
    justify-content: center;
    align-items: center;
}

.visual-container {
    position: relative;
    width: 300px;
    height: 300px;
}

.main-circle {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 120px;
    height: 120px;
    background: linear-gradient(135deg, #2e7d32, #4caf50);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 10px 30px rgba(46, 125, 50, 0.3);
    animation: main-float 4s ease-in-out infinite;
}

@keyframes main-float {

    0%,
    100% {
        transform: translate(-50%, -50%) scale(1);
    }

    50% {
        transform: translate(-50%, -50%) scale(1.05);
    }
}

.orbit-circle {
    position: absolute;
    width: 60px;
    height: 60px;
    background: white;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    animation: orbit 8s linear infinite;
}

.orbit-1 {
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    animation-delay: 0s;
}

.orbit-2 {
    top: 50%;
    right: 0;
    transform: translateY(-50%);
    animation-delay: 2s;
}

.orbit-3 {
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    animation-delay: 4s;
}

.orbit-4 {
    top: 50%;
    left: 0;
    transform: translateY(-50%);
    animation-delay: 6s;
}

@keyframes orbit {
    0% {
        transform: rotate(0deg) translateX(120px) rotate(0deg);
    }

    100% {
        transform: rotate(360deg) translateX(120px) rotate(-360deg);
    }
}

/* Features Section */
.features-section {
    position: relative;
    padding: 100px 0;
    background: linear-gradient(135deg, #1b5e20 0%, #2e7d32 100%);
    color: white;
    overflow: hidden;
}

.features-background {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
}

.bg-pattern {
    position: absolute;
    width: 100%;
    height: 100%;
    background-image: radial-gradient(circle at 25% 25%, rgba(255, 255, 255, 0.1) 0%, transparent 50%),
        radial-gradient(circle at 75% 75%, rgba(255, 255, 255, 0.1) 0%, transparent 50%);
}

.section-header {
    text-align: center;
    margin-bottom: 80px;
    position: relative;
    z-index: 2;
}

.section-title {
    font-size: 2.8rem;
    font-weight: 700;
    margin-bottom: 20px;
}

.section-description {
    font-size: 1.2rem;
    opacity: 0.9;
    max-width: 600px;
    margin: 0 auto;
}

.features-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 30px;
    position: relative;
    z-index: 2;
}

.feature-card {
    position: relative;
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
    border-radius: 20px;
    padding: 40px 30px;
    text-align: center;
    transition: all 0.3s ease;
    overflow: hidden;
}

.feature-card:hover {
    transform: translateY(-10px);
    background: rgba(255, 255, 255, 0.15);
}

.feature-card:hover .feature-hover-effect {
    transform: scale(1);
    opacity: 0.1;
}

.feature-hover-effect {
    position: absolute;
    top: -50%;
    left: -50%;
    width: 200%;
    height: 200%;
    background: radial-gradient(circle, rgba(255, 255, 255, 0.3) 0%, transparent 70%);
    transform: scale(0);
    opacity: 0;
    transition: all 0.3s ease;
    pointer-events: none;
}

.feature-icon {
    width: 80px;
    height: 80px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto 25px;
    position: relative;
    z-index: 2;
}

.feature-content {
    position: relative;
    z-index: 2;
}

.feature-title {
    font-size: 1.4rem;
    font-weight: 600;
    margin-bottom: 15px;
    color: white;
}

.feature-description {
    font-size: 1rem;
    line-height: 1.6;
    opacity: 0.9;
    color: white;
}

/* CTA Section */
.cta-section {
    padding: 100px 0;
    background: linear-gradient(135deg, #2e7d32 0%, #388e3c 50%, #4caf50 100%);
    color: white;
    text-align: center;
    position: relative;
    overflow: hidden;
}

.cta-section::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: url('data:image/svg+xml;utf8,<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg"><defs><pattern id="grain" width="100" height="100" patternUnits="userSpaceOnUse"><circle cx="25" cy="25" r="1" fill="rgba(255,255,255,0.1)"/><circle cx="75" cy="75" r="1" fill="rgba(255,255,255,0.1)"/><circle cx="50" cy="10" r="0.5" fill="rgba(255,255,255,0.1)"/><circle cx="20" cy="60" r="0.5" fill="rgba(255,255,255,0.1)"/><circle cx="80" cy="30" r="0.5" fill="rgba(255,255,255,0.1)"/><circle cx="40" cy="80" r="0.5" fill="rgba(255,255,255,0.1)"/></pattern></defs><rect width="100" height="100" fill="url(%23grain)"/></svg>') repeat;
    opacity: 0.3;
}

.cta-content {
    position: relative;
    z-index: 2;
    max-width: 800px;
    margin: 0 auto;
}

.cta-icon {
    margin-bottom: 30px;
    animation: cta-pulse 3s ease-in-out infinite;
}

@keyframes cta-pulse {

    0%,
    100% {
        transform: scale(1);
    }

    50% {
        transform: scale(1.1);
    }
}

.cta-title {
    font-size: 3rem;
    font-weight: 700;
    margin-bottom: 25px;
    line-height: 1.2;
}

.cta-description {
    font-size: 1.3rem;
    line-height: 1.7;
    margin-bottom: 50px;
    opacity: 0.95;
    max-width: 600px;
    margin-left: auto;
    margin-right: auto;
}

.cta-actions {
    display: flex;
    justify-content: center;
    gap: 25px;
    flex-wrap: wrap;
}

.cta-btn {
    padding: 20px 40px !important;
    font-size: 1.2rem !important;
    font-weight: 600 !important;
    border-radius: 35px !important;
    transition: all 0.3s ease !important;
    min-width: 220px;
}

.cta-btn.primary:hover {
    transform: translateY(-3px);
    box-shadow: 0 15px 40px rgba(0, 0, 0, 0.3);
}

.cta-btn.secondary:hover {
    transform: translateY(-3px);
    background: rgba(255, 255, 255, 0.1);
}

/* Responsive Design */
@media (max-width: 1200px) {
    .about-content {
        gap: 60px;
    }

    .features-grid {
        grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    }
}

@media (max-width: 960px) {
    .about-content {
        grid-template-columns: 1fr;
        gap: 50px;
        text-align: center;
    }

    .mission-values {
        max-width: 600px;
        margin: 0 auto;
    }

    .hero-stats {
        gap: 20px;
    }

    .stat-card {
        min-width: 120px;
        padding: 20px 15px;
    }
}

@media (max-width: 768px) {
    .title-main {
        font-size: 2.2rem;
    }

    .title-highlight {
        font-size: 3rem;
    }

    .hero-description {
        font-size: 1.1rem;
    }

    .hero-actions {
        flex-direction: column;
        align-items: center;
    }

    .main-btn,
    .secondary-btn {
        min-width: 250px;
    }

    .about-title {
        font-size: 2.2rem;
    }

    .section-title {
        font-size: 2.2rem;
    }

    .cta-title {
        font-size: 2.4rem;
    }

    .features-grid {
        grid-template-columns: 1fr;
    }

    .cta-actions {
        flex-direction: column;
        align-items: center;
    }
}

@media (max-width: 600px) {
    .hero-main {
        min-height: 90vh;
    }

    .hero-content {
        padding: 20px 15px;
    }

    .title-main {
        font-size: 1.8rem;
    }

    .title-highlight {
        font-size: 2.5rem;
    }

    .hero-subtitle {
        font-size: 1.2rem;
    }

    .hero-description {
        font-size: 1rem;
    }

    .hero-stats {
        flex-direction: column;
        align-items: center;
        gap: 15px;
    }

    .stat-card {
        width: 100%;
        max-width: 200px;
    }

    .value-item {
        flex-direction: column;
        text-align: center;
    }

    .about-section,
    .features-section,
    .cta-section {
        padding: 60px 0;
    }

    .visual-container {
        width: 250px;
        height: 250px;
    }

    .main-circle {
        width: 100px;
        height: 100px;
    }

    .orbit-circle {
        width: 50px;
        height: 50px;
    }
}

@media (max-width: 480px) {
    .hero-badge {
        padding: 10px 20px;
        gap: 8px;
    }

    .badge-pulse {
        width: 10px;
        height: 10px;
    }

    .feature-card {
        padding: 30px 20px;
    }

    .cta-btn {
        padding: 16px 30px !important;
        font-size: 1.1rem !important;
        min-width: 200px;
    }

    .section-header {
        margin-bottom: 50px;
    }
}

/* Print Styles */
@media print {
    .inicio-page {
        background: white !important;
        color: black !important;
    }

    .hero-main,
    .features-section,
    .cta-section {
        background: white !important;
        color: black !important;
    }

    .floating-elements,
    .sound-waves,
    .features-background {
        display: none !important;
    }

    .hero-badge,
    .stat-card,
    .feature-card {
        background: white !important;
        border: 1px solid #ccc !important;
    }
}

/* Accessibility */
@media (prefers-reduced-motion: reduce) {

    *,
    *::before,
    *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
    }
}

/* Dark mode support */
@media (prefers-color-scheme: dark) {
    .about-section {
        background: #1a1a1a;
    }

    .about-description p {
        color: #ccc;
    }

    .value-content p {
        color: #bbb;
    }
}

/* High contrast mode */
@media (prefers-contrast: high) {
    .hero-main {
        background: #000 !important;
        color: #fff !important;
    }

    .feature-card,
    .stat-card,
    .value-item {
        border: 2px solid #fff !important;
    }
}

/* Focus styles for keyboard navigation */
.main-btn:focus,
.secondary-btn:focus,
.cta-btn:focus {
    outline: 3px solid rgba(255, 255, 255, 0.6);
    outline-offset: 2px;
}

/* Smooth scrolling */
html {
    scroll-behavior: smooth;
}

/* Selection styles */
::selection {
    background: rgba(76, 175, 80, 0.3);
    color: inherit;
}

::-moz-selection {
    background: rgba(76, 175, 80, 0.3);
    color: inherit;
}
</style>