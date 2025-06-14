<template>
    <div class="creditos-page">
        <!-- Hero Section -->
        <section class="hero-section">
            <div class="hero-background">
                <div class="floating-icons">
                    <div class="floating-icon icon-1">💻</div>
                    <div class="floating-icon icon-2">🚀</div>
                    <div class="floating-icon icon-3">⚡</div>
                    <div class="floating-icon icon-4">🎨</div>
                    <div class="floating-icon icon-5">🔧</div>
                    <div class="floating-icon icon-6">✨</div>
                </div>
            </div>

            <v-container>
                <div class="hero-content">
                    <div class="hero-badge">
                        <v-icon class="pulse-icon">mdi-account-group</v-icon>
                        <span>NUESTRO EQUIPO</span>
                    </div>

                    <h1 class="hero-title">
                        Conoce a los
                        <span class="title-highlight">Creadores</span>
                    </h1>

                    <p class="hero-description">
                        Somos un equipo apasionado de estudiantes dedicados a crear
                        experiencias digitales excepcionales. Cada uno aporta su talento
                        único para hacer realidad este proyecto.
                    </p>

                    <div class="stats-container">
                        <div class="stat-item">
                            <div class="stat-number">{{ teamMembers.length }}</div>
                            <div class="stat-label">Desarrolladores</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-number">{{ totalSkills }}</div>
                            <div class="stat-label">Tecnologías</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-number">1</div>
                            <div class="stat-label">Proyecto</div>
                        </div>
                    </div>
                </div>
            </v-container>
        </section>

        <!-- Team Section -->
        <section class="team-section">
            <v-container>
                <div class="section-header">
                    <v-icon class="section-icon">mdi-account-star</v-icon>
                    <h2 class="section-title">Nuestro Equipo</h2>
                    <p class="section-description">
                        Los talentos detrás de este increíble proyecto
                    </p>
                </div>

                <div class="team-grid">
                    <v-card
                        v-for="(member, index) in teamMembers"
                        :key="member.id"
                        class="team-card"
                        :class="`card-${(index % 3) + 1}`"
                        elevation="8"
                        @click="showMemberDetails(member)"
                    >
                        <div class="card-background" :style="{ background: member.gradient }">
                            <div class="card-pattern"></div>
                        </div>

                        <div class="member-avatar">
                            <v-avatar size="120" class="avatar-container">
                                <v-img
                                    v-if="member.avatar"
                                    :src="member.avatar"
                                    :alt="member.name"
                                />
                                <v-icon v-else size="60" color="white">mdi-account</v-icon>
                            </v-avatar>
                            <div class="avatar-ring"></div>
                        </div>

                        <v-card-text class="member-content">
                            <div class="member-badge">
                                <v-chip size="small" :color="member.roleColor" variant="elevated">
                                    {{ member.role }}
                                </v-chip>
                            </div>

                            <h3 class="member-name">{{ member.name }}</h3>
                            <p class="member-title">{{ member.title }}</p>
                            <p class="member-description">{{ member.description }}</p>

                            <div class="skills-section">
                                <h4 class="skills-title">Especialidades</h4>
                                <div class="skills-list">
                                    <v-chip
                                        v-for="skill in member.skills.slice(0, 3)"
                                        :key="skill"
                                        size="small"
                                        variant="outlined"
                                        color="green"
                                        class="skill-chip"
                                    >
                                        {{ skill }}
                                    </v-chip>
                                    <v-chip
                                        v-if="member.skills.length > 3"
                                        size="small"
                                        variant="outlined"
                                        color="grey"
                                        class="skill-chip more-skills"
                                    >
                                        +{{ member.skills.length - 3 }}
                                    </v-chip>
                                </div>
                            </div>

                            <div class="member-stats">
                                <div class="stat">
                                    <v-icon size="small">mdi-code-tags</v-icon>
                                    <span>{{ member.contributions }} commits</span>
                                </div>
                                <div class="stat">
                                    <v-icon size="small">mdi-clock</v-icon>
                                    <span>{{ member.experience }}</span>
                                </div>
                            </div>

                            <div class="social-links">
                                <v-btn
                                    v-for="social in member.social"
                                    :key="social.platform"
                                    :icon="social.icon"
                                    size="small"
                                    variant="text"
                                    :color="social.color"
                                    class="social-btn"
                                    @click.stop="openSocialLink(social.url)"
                                />
                            </div>
                        </v-card-text>
                    </v-card>
                </div>
            </v-container>
        </section>

        <!-- Technologies Section -->
        <section class="tech-section">
            <v-container>
                <div class="section-header">
                    <v-icon class="section-icon">mdi-tools</v-icon>
                    <h2 class="section-title">Tecnologías Utilizadas</h2>
                    <p class="section-description">
                        Las herramientas que hacen posible este proyecto
                    </p>
                </div>

                <div class="tech-categories">
                    <div
                        v-for="category in techCategories"
                        :key="category.name"
                        class="tech-category"
                    >
                        <div class="category-header">
                            <v-icon :color="category.color" size="large">{{ category.icon }}</v-icon>
                            <h3 class="category-title">{{ category.name }}</h3>
                        </div>

                        <div class="tech-grid">
                            <div
                                v-for="tech in category.technologies"
                                :key="tech.name"
                                class="tech-item"
                                @click="showTechDetails(tech)"
                            >
                                <div class="tech-icon">
                                    <v-icon :color="tech.color" size="large">{{ tech.icon }}</v-icon>
                                </div>
                                <div class="tech-info">
                                    <h4 class="tech-name">{{ tech.name }}</h4>
                                    <p class="tech-description">{{ tech.description }}</p>
                                    <div class="tech-version">v{{ tech.version }}</div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </v-container>
        </section>

        <!-- Acknowledgments Section -->
        <section class="acknowledgments-section">
            <v-container>
                <div class="section-header">
                    <v-icon class="section-icon">mdi-heart</v-icon>
                    <h2 class="section-title">Agradecimientos</h2>
                    <p class="section-description">
                        A quienes hicieron posible este proyecto
                    </p>
                </div>

                <div class="acknowledgments-grid">
                    <v-card
                        v-for="ack in acknowledgments"
                        :key="ack.id"
                        class="ack-card"
                        elevation="4"
                    >
                        <div class="ack-icon">
                            <v-icon :color="ack.color" size="48">{{ ack.icon }}</v-icon>
                        </div>
                        <v-card-text class="ack-content">
                            <h3 class="ack-title">{{ ack.title }}</h3>
                            <p class="ack-description">{{ ack.description }}</p>
                        </v-card-text>
                    </v-card>
                </div>
            </v-container>
        </section>

        <!-- Contact Section -->
        <section class="contact-section">
            <v-container>
                <div class="contact-content">
                    <div class="contact-info">
                        <h2 class="contact-title">¿Tienes una idea genial?</h2>
                        <p class="contact-description">
                            Nos encanta colaborar en proyectos innovadores.
                            ¡Hablemos y hagamos realidad tu visión!
                        </p>

                        <div class="contact-methods">
                            <div class="contact-method">
                                <v-icon color="green">mdi-email</v-icon>
                                <span>ymorelochavez49@correo.unicordoba.edu.co</span>
                            </div>
                            <div class="contact-method">
                                <v-icon color="blue">mdi-github</v-icon>
                                <span>github.com/yeison-2000</span>
                            </div>
                        </div>
                    </div>

                    <div class="contact-illustration">
                        <div class="illustration-circle">
                            <v-icon size="120" color="green">mdi-rocket-launch</v-icon>
                        </div>
                    </div>
                </div>
            </v-container>
        </section>

        <!-- Member Details Dialog -->
        <v-dialog v-model="memberDialog" max-width="800px">
            <v-card v-if="selectedMember" class="member-dialog">
                <div class="dialog-header" :style="{ background: selectedMember.gradient }">
                    <div class="dialog-avatar">
                        <v-avatar size="80">
                            <v-img
                                v-if="selectedMember.avatar"
                                :src="selectedMember.avatar"
                                :alt="selectedMember.name"
                            />
                            <v-icon v-else size="40" color="white">mdi-account</v-icon>
                        </v-avatar>
                    </div>
                    <div class="dialog-info">
                        <h2 class="dialog-name">{{ selectedMember.name }}</h2>
                        <p class="dialog-title">{{ selectedMember.title }}</p>
                    </div>
                    <v-spacer></v-spacer>
                    <v-btn icon variant="text" color="white" @click="memberDialog = false">
                        <v-icon>mdi-close</v-icon>
                    </v-btn>
                </div>

                <v-card-text class="dialog-content">
                    <div class="dialog-section">
                        <h3 class="section-subtitle">Sobre mí</h3>
                        <p class="dialog-bio">{{ selectedMember.bio }}</p>
                    </div>

                    <div class="dialog-section">
                        <h3 class="section-subtitle">Todas las especialidades</h3>
                        <div class="all-skills">
                            <v-chip
                                v-for="skill in selectedMember.skills"
                                :key="skill"
                                class="ma-1"
                                color="green"
                                variant="outlined"
                            >
                                {{ skill }}
                            </v-chip>
                        </div>
                    </div>

                    <div class="dialog-section">
                        <h3 class="section-subtitle">Proyectos destacados</h3>
                        <div class="projects-list">
                            <div
                                v-for="project in selectedMember.projects"
                                :key="project.name"
                                class="project-item"
                            >
                                <h4 class="project-name">{{ project.name }}</h4>
                                <p class="project-description">{{ project.description }}</p>
                            </div>
                        </div>
                    </div>
                </v-card-text>
            </v-card>
        </v-dialog>
    </div>
</template>

<script>
export default {
    name: "CreditosPage",

    data() {
        return {
            memberDialog: false,
            selectedMember: null,

            teamMembers: [
                {
                    id: 1,
                    name: "Yeison Morelo Chávez",
                    title: "Frontend Developer & UX Designer",
                    role: "LÍDER FRONTEND",
                    roleColor: "purple",
                    description: "Especialista en crear interfaces intuitivas y experiencias de usuario excepcionales.",
                    bio: "Con poca experiencia en desarrollo frontend, Yeison se especializa en Vue.js y diseño UX/UI. Su pasión por crear interfaces hermosas y funcionales la convierte en el corazón creativo del equipo.",
                    avatar: `/img/Yeison.png`,
                    gradient: "linear-gradient(135deg, #667eea 0%, #764ba2 100%)",
                    skills: ["Vue.js", "Vuetify", "UX/UI Design", "CSS3", "JavaScript", "node.js", "git"],
                    contributions: 247,
                    experience: "3 años",
                    social: [
                        { platform: "GitHub", icon: "mdi-github", color: "black", url: "github.com/yeison-2000" },
                        { platform: "LinkedIn", icon: "mdi-linkedin", color: "blue", url: "https://www.linkedin.com/in/yeison-morelo-784853354/" },
                    ],
                    projects: [
                        { name: "RANDOM FOREST - OVA", description: "Interfaz completa del ova" },
                        { name: "PAGINA RADIO ESCOLAR SMG", description: "Progama radial de la institución educativa Santa María Goretti" }
                    ]
                },
                {
                    id: 2,
                    name: "Jesús David González ",
                    title: "Lider de producción y edición de audio",
                    role: "LIDER AUDIO",
                    roleColor: "orange",
                    description: "Experto en producción y edición de audio, asegurando la calidad de nuestras grabaciones.",
                    bio: "Jesus es nuestro experto en sonido. Con una gran habilidad para la producción y edición de audio, se asegura de que cada grabación suene perfecta. Su atención al detalle y creatividad son esenciales para el éxito de nuestros proyectos.",
                    avatar: `/img/jesus.jpg`,
                    gradient: "linear-gradient(135deg, #f093fb 0%, #f5576c 100%)",
                    skills: ["Audacity", "Adobe audition"],
                    contributions: 189,
                    experience: "3 años",
                    projects: [
                        { name: "NOTICIERO SMG", description: "Noticiero escolar de la IE Santa María Goretti" },
                        { name: "RADIONOVELA", description: "Radionovela ´ecos del ultimo codigo`" }
                    ],
                    social: [
                        { platform: "GitHub", icon: "mdi-github", color: "black", url: "https://github.com/JESULIKE" },
                    ],
                },
                {
                    id: 3,
                    name: "Yuliana Julian Otero Carmona",
                    title: "Voz femenina principal",
                    role: "VOICE",
                    roleColor: "green",
                    description: "Voz femenina principal del equipo, aportando su talento a nuestras grabaciones.",
                    bio: "Yuliana es la voz que da vida a nuestros proyectos. Con su talento vocal, aporta una dimensión única a nuestras grabaciones. Su dedicación y profesionalismo son clave para lograr resultados excepcionales.",
                    avatar: `/img/yuliana-otero.jpg`,	
                    gradient: "linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)",
                    skills: ["Audacity", "Adobe audition", "Voz en off", "Locución"],
                    contributions: 203,
                    experience: "3 años",
                    projects: [
                        { name: "RADIONOVELA", description: "Radionovela ´ecos del ultimo codigo`" },
                        { name: "PODCAST", description: "Podcast institucional de la IE Santa María Goretti" }
                    ],
                },
                {
                    id: 4,
                    name: "Jander Ensuncho Pérez",
                    title: "Talento musical",
                    role: "MUSIC",
                    roleColor: "blue",
                    description: "Músico y compositor, encargado de la producción musical de nuestros proyectos.",
                    bio: "Jander es nuestro genio musical. Con su talento para componer y producir música, añade una capa especial a nuestras grabaciones. Su creatividad y pasión por la música enriquecen cada proyecto en el que trabaja.",
                    avatar: `/img/jander.jpg`,	
                    gradient: "linear-gradient(135deg, #a8edea 0%, #fed6e3 100%)",
                    skills: ["Producción Musical", "Composición", "Guitarra", "Piano", "Ableton Live", "FL Studio"],
                    contributions: 156,
                    experience: "3 años",
                    social: [
                        { platform: "GitHub", icon: "mdi-github", color: "black", url: "https://github.com/jensunchoperez" },
                    ],
                    projects: [
                        { name: "RADIONOVELA", description: "Radionovela ´ecos del ultimo codigo`" },
                        { name: "PODCAST", description: "Podcast institucional de la IE Santa María Goretti" }
                    ]
                },
                {
                    id: 5,
                    name: "Carlos Steven Morales Padilla",
                    title: "Voz masculina principal",
                    role: "VOICE",
                    roleColor: "teal",
                    description: "Voz masculina principal del equipo, aportando su talento a nuestras grabaciones.",
                    bio: "Carlos Steven es la voz masculina que complementa nuestro equipo. Con su habilidad vocal, aporta profundidad y carácter a nuestras grabaciones. Su profesionalismo y dedicación son esenciales para lograr resultados excepcionales.",
                    avatar: `/img/steven.jpg`,
                    gradient: "linear-gradient(135deg, #d299c2 0%, #fef9d7 100%)",
                    skills: ["Audacity", "Adobe audition", "Voz en off", "Locución"],
                    contributions: 98,
                    experience: "3 años",
                    projects: [
                        { name: "RADIONOVELA", description: "Radionovela ´ecos del ultimo codigo`" },
                        { name: "PODCAST", description: "Podcast institucional de la IE Santa María Goretti" }
                    ]
                },
                {
                    id: 6,
                    name: "Pedro Luis Romero Maquez",
                    title: "Voz masculina secundaria",
                    role: "VOICE",
                    roleColor: "red",
                    description: "Voz masculina secundaria del equipo, aportando su talento a nuestras grabaciones.",
                    bio: "  Pedro Luis es una voz versátil que complementa nuestro equipo. Con su habilidad vocal, aporta matices y variedad a nuestras grabaciones. Su dedicación y profesionalismo son clave para lograr resultados excepcionales.",
                    avatar: `/img/pedro.png`,
                    gradient: "linear-gradient(135deg, #89f7fe 0%, #66a6ff 100%)",
                    skills: ["Audacity", "Adobe audition", "Voz en off", "Locución"],
                    contributions: 134,
                    experience: "3 años",
                    social: [
                    ],
                    projects: [
                        { name: "RADIONOVELA", description: "Radionovela ´ecos del ultimo codigo`" },
                        { name: "PODCAST", description: "Podcast institucional de la IE Santa María Goretti" }
                    ]
                }
            ],

            techCategories: [
                {
                    name: "Frontend",
                    icon: "mdi-web",
                    color: "blue",
                    technologies: [
                        { name: "Vue.js", description: "Framework progresivo", icon: "mdi-vuejs", color: "green", version: "3.0" },
                        { name: "Vuetify", description: "Material Design", icon: "mdi-material-design", color: "blue", version: "3.4" },
                        { name: "JavaScript", description: "Lenguaje principal", icon: "mdi-language-javascript", color: "yellow", version: "ES2023" }
                    ]
                },
                {
                    name: "Backend",
                    icon: "mdi-server",
                    color: "orange",
                    technologies: [
                        { name: "Node.js", description: "Runtime de JavaScript", icon: "mdi-nodejs", color: "green", version: "18.0" },
                        { name: "Express", description: "Framework web", icon: "mdi-web", color: "grey", version: "4.18" },
                    ]
                },
                {
                    name: "Herramientas",
                    icon: "mdi-tools",
                    color: "purple",
                    technologies: [
                        { name: "Git", description: "Control de versiones", icon: "mdi-git", color: "orange", version: "2.40" },
                        { name: "Docker", description: "Contenedorización", icon: "mdi-docker", color: "blue", version: "24.0" },
                        { name: "VS Code", description: "Editor de código", icon: "mdi-microsoft-visual-studio-code", color: "blue", version: "1.85" }
                    ]
                }
            ],

            acknowledgments: [
                {
                    id: 1,
                    title: "Institución Educativa",
                    description: "Por brindarnos la oportunidad de contribuir al crecimiento digital de la comunidad educativa.",
                    icon: "mdi-school",
                    color: "green"
                },
                {
                    id: 2,
                    title: "Comunidad Open Source",
                    description: "A todos los desarrolladores que comparten sus conocimientos y herramientas libremente.",
                    icon: "mdi-open-source-initiative",
                    color: "blue"
                },
                {
                    id: 3,
                    title: "Mentores y Profesores",
                    description: "Quienes nos guiaron en este camino del desarrollo y nos inspiraron a crear soluciones innovadoras.",
                    icon: "mdi-account-tie",
                    color: "purple"
                },
                {
                    id: 4,
                    title: "Familia y Amigos",
                    description: "Por su apoyo incondicional durante las largas noches de Grabación y código.",
                    icon: "mdi-heart",
                    color: "red"
                }
            ]
        };
    },

    computed: {
        totalSkills() {
            const allSkills = this.teamMembers.flatMap(member => member.skills);
            return [...new Set(allSkills)].length;
        }
    },

    methods: {
        showMemberDetails(member) {
            this.selectedMember = member;
            this.memberDialog = true;
        },

        openSocialLink(url) {
            if (url !== '#') {
                window.open(url, '_blank');
            }
        },

        showTechDetails(tech) {
            console.log('Mostrar detalles de:', tech.name);
        }
    }
};
</script>

<style scoped>
.creditos-page {
    min-height: 100vh;
    background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
}

/* Hero Section - Similar to gallery */
.hero-section {
    position: relative;
    padding: 80px 0;
    background: linear-gradient(135deg, #1b5e20 0%, #2e7d32 50%, #1b5e20 100%);
    color: white;
    overflow: hidden;
}

.hero-background {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    opacity: 0.1;
}

.floating-icons {
    position: absolute;
    width: 100%;
    height: 100%;
}

.floating-icon {
    position: absolute;
    font-size: 3rem;
    animation: float 6s ease-in-out infinite;
}

.icon-1 { top: 20%; left: 10%; animation-delay: 0s; }
.icon-2 { top: 30%; right: 15%; animation-delay: 1s; }
.icon-3 { bottom: 40%; left: 20%; animation-delay: 2s; }
.icon-4 { top: 60%; right: 25%; animation-delay: 3s; }
.icon-5 { bottom: 20%; right: 10%; animation-delay: 4s; }
.icon-6 { top: 70%; left: 30%; animation-delay: 5s; }

@keyframes float {
    0%, 100% { transform: translateY(0px) rotate(0deg); }
    25% { transform: translateY(-20px) rotate(5deg); }
    50% { transform: translateY(-10px) rotate(-5deg); }
    75% { transform: translateY(-15px) rotate(3deg); }
}

.hero-content {
    position: relative;
    z-index: 2;
    text-align: center;
    max-width: 800px;
    margin: 0 auto;
}

.hero-badge {
    display: inline-flex;
    align-items: center;
    gap: 10px;
    background: rgba(255, 255, 255, 0.1);
    padding: 8px 20px;
    border-radius: 25px;
    margin-bottom: 20px;
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
}

.pulse-icon {
    animation: pulse 1.5s ease-in-out infinite;
    color: #4caf50;
}

@keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.7; transform: scale(1.1); }
}

.hero-title {
    font-size: 3.5rem;
    font-weight: 800;
    margin-bottom: 20px;
    line-height: 1.1;
}

.title-highlight {
    background: linear-gradient(45deg, #81c784, #c8e6c9);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

.hero-description {
    font-size: 1.2rem;
    opacity: 0.9;
    margin-bottom: 40px;
    line-height: 1.6;
}

.stats-container {
    display: flex;
    justify-content: center;
    gap: 40px;
    flex-wrap: wrap;
}

.stat-item {
    text-align: center;
}

.stat-number {
    font-size: 2.5rem;
    font-weight: 700;
    color: #81c784;
    margin-bottom: 5px;
}

.stat-label {
    font-size: 1rem;
    opacity: 0.8;
    text-transform: uppercase;
    letter-spacing: 1px;
}

/* Section Headers */
.section-header {
    text-align: center;
    margin-bottom: 50px;
}

.section-icon {
    font-size: 3rem;
    color: #2e7d32;
    margin-bottom: 15px;
}

.section-title {
    font-size: 2.5rem;
    font-weight: 700;
    color: #1b5e20;
    margin-bottom: 15px;
}

.section-description {
    font-size: 1.2rem;
    color: #666;
    max-width: 600px;
    margin: 0 auto;
}

/* Team Section */
.team-section {
    padding: 80px 0;
    background: white;
}

.team-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 30px;
}

.team-card {
    position: relative;
    border-radius: 20px;
    overflow: hidden;
    cursor: pointer;
    transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    border: none;
    min-height: 500px;
}

.team-card:hover {
    transform: translateY(-15px) scale(1.02);
    box-shadow: 0 25px 50px rgba(0, 0, 0, 0.15);
}

.card-background {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    opacity: 0.9;
}

.card-pattern {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-image: 
        radial-gradient(circle at 25% 25%, rgba(255,255,255,0.1) 0%, transparent 50%),
        radial-gradient(circle at 75% 75%, rgba(255,255,255,0.1) 0%, transparent 50%);
}

.member-avatar {
    position: relative;
    text-align: center;
    padding: 30px 0 20px;
}

.avatar-container {
    position: relative;
    z-index: 2;
    border: 4px solid rgba(255, 255, 255, 0.3);
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
}

.avatar-ring {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 140px;
    height: 140px;
    border: 2px solid rgba(255, 255, 255, 0.2);
    border-radius: 50%;
    animation: rotate 8s linear infinite;
}

@keyframes rotate {
    from { transform: translate(-50%, -50%) rotate(0deg); }
    to { transform: translate(-50%, -50%) rotate(360deg); }
}

.member-content {
    position: relative;
    z-index: 2;
    color: white;
    text-align: center;
    padding: 0 25px 25px;
}

.member-badge {
    margin-bottom: 15px;
}

.member-name {
    font-size: 1.8rem;
    font-weight: 700;
    margin-bottom: 8px;
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.member-title {
    font-size: 1.1rem;
    opacity: 0.9;
    margin-bottom: 15px;
    font-weight: 500;
}

.member-description {
    font-size: 0.95rem;
    line-height: 1.5;
    opacity: 0.8;
    margin-bottom: 20px;
}

.skills-section {
    margin-bottom: 20px;
}

.skills-title {
    font-size: 1rem;
    font-weight: 600;
    margin-bottom: 10px;
    text-transform: uppercase;
    letter-spacing: 1px;
}

.skills-list {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    justify-content: center;
}

.skill-chip {
    background: rgba(255, 255, 255, 0.15) !important;
    color: white !important;
    border-color: rgba(255, 255, 255, 0.3) !important;
    backdrop-filter: blur(10px);
}

.more-skills {
    background: rgba(255, 255, 255, 0.2) !important;
}

.member-stats {
    display: flex;
    justify-content: space-around;
    margin-bottom: 20px;
    padding: 15px 0;
    border-top: 1px solid rgba(255, 255, 255, 0.2);
    border-bottom: 1px solid rgba(255, 255, 255, 0.2);
}

.stat {
    display: flex;
    align-items: center;
    gap: 5px;
    font-size: 0.9rem;
    opacity: 0.9;
}

.social-links {
    display: flex;
    justify-content: center;
    gap: 10px;
}

.social-btn {
    background: rgba(255, 255, 255, 0.1) !important;
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
}

.social-btn:hover {
    background: rgba(255, 255, 255, 0.2) !important;
    transform: scale(1.1);
}

/* Tech Section */
.tech-section {
    padding: 80px 0;
    background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
}

.tech-categories {
    display: flex;
    flex-direction: column;
    gap: 50px;
}

.tech-category {
    background: white;
    border-radius: 20px;
    padding: 40px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease;
}

.tech-category:hover {
    transform: translateY(-5px);
}

.category-header {
    display: flex;
    align-items: center;
    gap: 20px;
    margin-bottom: 30px;
    padding-bottom: 20px;
    border-bottom: 2px solid #f0f0f0;
}

.category-title {
    font-size: 2rem;
    font-weight: 700;
    color: #2e7d32;
    margin: 0;
}

.tech-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
}

.tech-item {
    display: flex;
    align-items: center;
    gap: 20px;
    padding: 20px;
    background: #f8f9fa;
    border-radius: 15px;
    cursor: pointer;
    transition: all 0.3s ease;
    border: 2px solid transparent;
}

.tech-item:hover {
    background: white;
    border-color: #2e7d32;
    box-shadow: 0 5px 20px rgba(46, 125, 50, 0.15);
    transform: translateX(5px);
}

.tech-icon {
    flex-shrink: 0;
    width: 60px;
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: white;
    border-radius: 12px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.tech-info {
    flex: 1;
}

.tech-name {
    font-size: 1.3rem;
    font-weight: 600;
    color: #2e7d32;
    margin-bottom: 5px;
}

.tech-description {
    font-size: 1rem;
    color: #666;
    margin-bottom: 8px;
}

.tech-version {
    font-size: 0.9rem;
    color: #999;
    font-weight: 500;
}

/* Acknowledgments Section */
.acknowledgments-section {
    padding: 80px 0;
    background: linear-gradient(135deg, #2e7d32 0%, #1b5e20 100%);
    color: white;
}

.acknowledgments-section .section-icon,
.acknowledgments-section .section-title {
    color: white;
}

.acknowledgments-section .section-description {
    color: rgba(255, 255, 255, 0.8);
}

.acknowledgments-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 30px;
}

.ack-card {
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
    border-radius: 20px;
    text-align: center;
    padding: 30px 20px;
    transition: all 0.3s ease;
    color: white;
}

.ack-card:hover {
    background: rgba(255, 255, 255, 0.15);
    transform: translateY(-10px);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.2);
}

.ack-icon {
    margin-bottom: 20px;
}

.ack-content {
    color: white;
}

.ack-title {
    font-size: 1.4rem;
    font-weight: 600;
    margin-bottom: 15px;
    color: white;
}

.ack-description {
    font-size: 1rem;
    line-height: 1.6;
    opacity: 0.9;
    color: white;
}

/* Contact Section */
.contact-section {
    padding: 80px 0;
    background: white;
}

.contact-content {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 60px;
    align-items: center;
    max-width: 1000px;
    margin: 0 auto;
}

.contact-title {
    font-size: 2.5rem;
    font-weight: 700;
    color: #1b5e20;
    margin-bottom: 20px;
}

.contact-description {
    font-size: 1.2rem;
    color: #666;
    line-height: 1.6;
    margin-bottom: 30px;
}

.contact-methods {
    display: flex;
    flex-direction: column;
    gap: 15px;
}

.contact-method {
    display: flex;
    align-items: center;
    gap: 15px;
    font-size: 1.1rem;
    color: #2e7d32;
    font-weight: 500;
}

.contact-illustration {
    display: flex;
    justify-content: center;
    align-items: center;
}

.illustration-circle {
    width: 300px;
    height: 300px;
    background: linear-gradient(135deg, #81c784 0%, #4caf50 100%);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    animation: float 3s ease-in-out infinite;
    box-shadow: 0 20px 40px rgba(76, 175, 80, 0.3);
}

/* Member Dialog */
.member-dialog {
    border-radius: 20px;
    overflow: hidden;
}

.dialog-header {
    padding: 30px;
    color: white;
    display: flex;
    align-items: center;
    gap: 20px;
}

.dialog-avatar .v-avatar {
    border: 3px solid rgba(255, 255, 255, 0.3);
}

.dialog-name {
    font-size: 2rem;
    font-weight: 700;
    margin-bottom: 5px;
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.dialog-title {
    font-size: 1.2rem;
    opacity: 0.9;
}

.dialog-content {
    padding: 40px;
}

.dialog-section {
    margin-bottom: 30px;
}

.section-subtitle {
    font-size: 1.4rem;
    font-weight: 600;
    color: #2e7d32;
    margin-bottom: 15px;
    border-bottom: 2px solid #e0e0e0;
    padding-bottom: 5px;
}

.dialog-bio {
    font-size: 1.1rem;
    line-height: 1.7;
    color: #555;
}

.all-skills {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
}

.projects-list {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.project-item {
    padding: 20px;
    background: #f8f9fa;
    border-radius: 12px;
    border-left: 4px solid #2e7d32;
}

.project-name {
    font-size: 1.2rem;
    font-weight: 600;
    color: #2e7d32;
    margin-bottom: 8px;
}

.project-description {
    font-size: 1rem;
    color: #666;
    line-height: 1.5;
}

/* Responsive Design */
@media (max-width: 768px) {
    .hero-title {
        font-size: 2.5rem;
    }
    
    .stats-container {
        gap: 20px;
    }
    
    .team-grid {
        grid-template-columns: 1fr;
    }
    
    .contact-content {
        grid-template-columns: 1fr;
        gap: 40px;
        text-align: center;
    }
    
    .category-header {
        flex-direction: column;
        text-align: center;
        gap: 15px;
    }
    
    .tech-grid {
        grid-template-columns: 1fr;
    }
    
    .acknowledgments-grid {
        grid-template-columns: 1fr;
    }
    
    .illustration-circle {
        width: 200px;
        height: 200px;
    }
}

@media (max-width: 480px) {
    .hero-section {
        padding: 60px 0;
    }
    
    .hero-title {
        font-size: 2rem;
    }
    
    .section-title {
        font-size: 2rem;
    }
    
    .team-card {
        min-height: 450px;
    }
    
    .member-name {
        font-size: 1.5rem;
    }
    
    .contact-title {
        font-size: 2rem;
    }
}
</style>