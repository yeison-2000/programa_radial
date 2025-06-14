<template>
    <div class="programas-page">
        <!-- Hero Section -->
        <section class="hero-section">
            <div class="hero-background">
                <div class="sound-waves">
                    <div class="wave wave-1"></div>
                    <div class="wave wave-2"></div>
                    <div class="wave wave-3"></div>
                    <div class="wave wave-4"></div>
                </div>
                <div class="floating-notes">
                    <div class="note note-1">♪</div>
                    <div class="note note-2">♫</div>
                    <div class="note note-3">♪</div>
                    <div class="note note-4">♫</div>
                    <div class="note note-5">♪</div>
                </div>
            </div>

            <v-container>
                <div class="hero-content">
                    <div class="hero-badge">
                        <v-icon class="radio-icon">mdi-radio</v-icon>
                        <span>NUESTROS PROGRAMAS</span>
                    </div>

                    <h1 class="hero-title">
                        Voces que
                        <span class="title-highlight">Conectan</span>
                    </h1>

                    <p class="hero-description">
                        Descubre nuestros programas radiales únicos, creados con pasión 
                        por estudiantes para la comunidad educativa. Desde noticias hasta 
                        entretenimiento, cada programa refleja nuestra creatividad y compromiso.
                    </p>

                    <div class="hero-stats">
                        <div class="stat-item">
                            <div class="stat-number">{{ totalPrograms }}</div>
                            <div class="stat-label">Programas</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-number">{{ totalDuration }}</div>
                            <div class="stat-label">Minutos</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-number">{{ totalListeners }}</div>
                            <div class="stat-label">Oyentes</div>
                        </div>
                    </div>

                    <v-btn
                        size="large"
                        color="white"
                        variant="elevated"
                        class="explore-btn"
                        @click="scrollToPrograms"
                    >
                        <v-icon start>mdi-play</v-icon>
                        Explorar Programas
                    </v-btn>
                </div>
            </v-container>
        </section>

        <!-- Programs Section -->
        <section class="programs-section" ref="programsSection">
            <v-container>
                <div class="section-header">
                    <v-icon class="section-icon">mdi-microphone</v-icon>
                    <h2 class="section-title">Nuestras Producciones</h2>
                    <p class="section-description">
                        Cada programa es una ventana a diferentes aspectos de nuestra vida escolar
                    </p>
                </div>

                <div class="programs-grid">
                    <v-card
                        v-for="(program, index) in programs"
                        :key="program.id"
                        class="program-card"
                        :class="`program-${index + 1}`"
                        elevation="12"
                        @click="selectProgram(program)"
                    >
                        <div class="card-header" :style="{ background: program.gradient }">
                            <div class="header-pattern"></div>
                            <div class="program-icon">
                                <v-icon size="x-large" color="white">{{ program.icon }}</v-icon>
                            </div>
                            <div class="program-category">{{ program.category }}</div>
                        </div>

                        <v-card-text class="program-content">
                            <div class="program-title-section">
                                <h3 class="program-title">{{ program.title }}</h3>
                                <div class="program-subtitle">{{ program.subtitle }}</div>
                            </div>

                            <p class="program-description">{{ program.description }}</p>

                            <div class="program-details">
                                <div class="detail-item">
                                    <v-icon size="small" color="green">mdi-clock</v-icon>
                                    <span>{{ program.duration }}</span>
                                </div>
                                <div class="detail-item">
                                    <v-icon size="small" color="blue">mdi-account-group</v-icon>
                                    <span>{{ program.hosts }}</span>
                                </div>
                                <div class="detail-item">
                                    <v-icon size="small" color="orange">mdi-calendar</v-icon>
                                    <span>{{ program.date }}</span>
                                </div>
                            </div>

                            <div class="program-features">
                                <v-chip
                                    v-for="feature in program.features"
                                    :key="feature"
                                    size="small"
                                    color="green"
                                    variant="outlined"
                                    class="feature-chip"
                                >
                                    {{ feature }}
                                </v-chip>
                            </div>

                            <div class="program-actions">
                                <v-btn
                                    :color="program.color"
                                    variant="elevated"
                                    size="large"
                                    class="play-btn"
                                    :loading="currentlyPlaying === program.id"
                                    @click.stop="togglePlayback(program)"
                                >
                                    <v-icon start>
                                        {{ currentlyPlaying === program.id ? 'mdi-pause' : 'mdi-play' }}
                                    </v-icon>
                                    {{ currentlyPlaying === program.id ? 'Pausar' : 'Escuchar' }}
                                </v-btn>

                                <v-btn
                                    variant="outlined"
                                    :color="program.color"
                                    size="large"
                                    @click.stop="showProgramDetails(program)"
                                >
                                    <v-icon start>mdi-information</v-icon>
                                    Detalles
                                </v-btn>
                            </div>
                        </v-card-text>
                    </v-card>
                </div>
            </v-container>
        </section>

        <!-- Featured Section -->
        <section class="featured-section">
            <v-container>
                <div class="featured-content">
                    <div class="featured-text">
                        <h2 class="featured-title">Producción Estudiantil</h2>
                        <p class="featured-description">
                            Cada programa es el resultado del trabajo colaborativo de nuestros 
                            estudiantes, quienes se encargan de la investigación, guionización, 
                            locución y edición. Una experiencia integral que combina creatividad, 
                            tecnología y comunicación.
                        </p>
                        
                        <div class="featured-highlights">
                            <div class="highlight-item">
                                <v-icon color="green" size="large">mdi-microphone-variant</v-icon>
                                <div>
                                    <h4>Locución Profesional</h4>
                                    <p>Estudiantes capacitados en técnicas de radio</p>
                                </div>
                            </div>
                            <div class="highlight-item">
                                <v-icon color="blue" size="large">mdi-script-text</v-icon>
                                <div>
                                    <h4>Guiones Originales</h4>
                                    <p>Contenido 100% creado por nuestro equipo</p>
                                </div>
                            </div>
                            <div class="highlight-item">
                                <v-icon color="orange" size="large">mdi-music-note</v-icon>
                                <div>
                                    <h4>Producción Musical</h4>
                                    <p>Efectos sonoros y música original</p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="featured-visual">
                        <div class="studio-illustration">
                            <div class="studio-circle main-circle">
                                <v-icon size="80" color="white">mdi-radio-tower</v-icon>
                            </div>
                            <div class="studio-circle circle-1">
                                <v-icon size="30" color="green">mdi-microphone</v-icon>
                            </div>
                            <div class="studio-circle circle-2">
                                <v-icon size="30" color="blue">mdi-headphones</v-icon>
                            </div>
                            <div class="studio-circle circle-3">
                                <v-icon size="30" color="orange">mdi-volume-high</v-icon>
                            </div>
                        </div>
                    </div>
                </div>
            </v-container>
        </section>

        <!-- Audio Player Section -->
        <section class="player-section" v-if="selectedAudio">
            <v-container>
                <v-card class="audio-player" elevation="8">
                    <div class="player-header">
                        <div class="now-playing">
                            <v-icon color="green" class="pulse-icon">mdi-radio</v-icon>
                            <span>Reproduciendo ahora</span>
                        </div>
                        <v-btn
                            icon
                            variant="text"
                            @click="closePlayer"
                        >
                            <v-icon>mdi-close</v-icon>
                        </v-btn>
                    </div>

                    <div class="player-content">
                        <div class="player-info">
                            <h3 class="player-title">{{ selectedAudio.title }}</h3>
                            <p class="player-subtitle">{{ selectedAudio.subtitle }}</p>
                        </div>

                        <div class="player-controls">
                            <audio
                                ref="audioPlayer"
                                :src="selectedAudio.audioUrl"
                                @timeupdate="updateProgress"
                                @loadedmetadata="setDuration"
                                @ended="audioEnded"
                            ></audio>

                            <div class="control-buttons">
                                <v-btn
                                    icon
                                    size="large"
                                    color="green"
                                    @click="skipBackward"
                                >
                                    <v-icon>mdi-skip-backward</v-icon>
                                </v-btn>

                                <v-btn
                                    icon
                                    size="x-large"
                                    color="green"
                                    variant="elevated"
                                    class="play-button"
                                    @click="toggleMainPlayback"
                                >
                                    <v-icon size="large">
                                        {{ isPlaying ? 'mdi-pause' : 'mdi-play' }}
                                    </v-icon>
                                </v-btn>

                                <v-btn
                                    icon
                                    size="large"
                                    color="green"
                                    @click="skipForward"
                                >
                                    <v-icon>mdi-skip-forward</v-icon>
                                </v-btn>
                            </div>

                            <div class="progress-section">
                                <span class="time-display">{{ formatTime(currentTime) }}</span>
                                <v-slider
                                    v-model="currentTime"
                                    :max="totalDurationSeconds"
                                    color="green"
                                    track-color="grey-lighten-2"
                                    thumb-color="green"
                                    class="progress-slider"
                                    @update:model-value="seekTo"
                                ></v-slider>
                                <span class="time-display">{{ formatTime(totalDurationSeconds) }}</span>
                            </div>

                            <div class="volume-section">
                                <v-icon color="grey">mdi-volume-high</v-icon>
                                <v-slider
                                    v-model="volume"
                                    :max="100"
                                    color="green"
                                    class="volume-slider"
                                    @update:model-value="setVolume"
                                ></v-slider>
                            </div>
                        </div>
                    </div>
                </v-card>
            </v-container>
        </section>

        <!-- Program Details Dialog -->
        <v-dialog v-model="detailsDialog" max-width="900px">
            <v-card v-if="selectedProgram" class="program-details-dialog">
                <div class="dialog-header" :style="{ background: selectedProgram.gradient }">
                    <div class="dialog-icon">
                        <v-icon size="x-large" color="white">{{ selectedProgram.icon }}</v-icon>
                    </div>
                    <div class="dialog-info">
                        <h2 class="dialog-title">{{ selectedProgram.title }}</h2>
                        <p class="dialog-subtitle">{{ selectedProgram.subtitle }}</p>
                    </div>
                    <v-spacer></v-spacer>
                    <v-btn icon variant="text" color="white" @click="detailsDialog = false">
                        <v-icon>mdi-close</v-icon>
                    </v-btn>
                </div>

                <v-card-text class="dialog-content">
                    <div class="dialog-section">
                        <h3 class="section-subtitle">Descripción del Programa</h3>
                        <p class="program-full-description">{{ selectedProgram.fullDescription }}</p>
                    </div>

                    <div class="dialog-section">
                        <h3 class="section-subtitle">Equipo de Producción</h3>
                        <div class="team-list">
                            <div
                                v-for="member in selectedProgram.team"
                                :key="member.name"
                                class="team-member"
                            >
                                <v-avatar size="40" color="green">
                                    <span class="text-white">{{ member.name.charAt(0) }}</span>
                                </v-avatar>
                                <div class="member-info">
                                    <h4 class="member-name">{{ member.name }}</h4>
                                    <p class="member-role">{{ member.role }}</p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="dialog-section">
                        <h3 class="section-subtitle">Detalles Técnicos</h3>
                        <div class="technical-details">
                            <div class="tech-item">
                                <strong>Duración:</strong> {{ selectedProgram.duration }}
                            </div>
                            <div class="tech-item">
                                <strong>Formato:</strong> {{ selectedProgram.format }}
                            </div>
                            <div class="tech-item">
                                <strong>Fecha de grabación:</strong> {{ selectedProgram.date }}
                            </div>
                            <div class="tech-item">
                                <strong>Herramientas utilizadas:</strong> {{ selectedProgram.tools.join(', ') }}
                            </div>
                        </div>
                    </div>

                    <div class="dialog-section">
                        <h3 class="section-subtitle">Segmentos Destacados</h3>
                        <div class="segments-list">
                            <div
                                v-for="segment in selectedProgram.segments"
                                :key="segment.name"
                                class="segment-item"
                            >
                                <div class="segment-time">{{ segment.time }}</div>
                                <div class="segment-info">
                                    <h4 class="segment-name">{{ segment.name }}</h4>
                                    <p class="segment-description">{{ segment.description }}</p>
                                </div>
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
    name: "ProgramasPage",

    data() {
        return {
            detailsDialog: false,
            selectedProgram: null,
            selectedAudio: null,
            currentlyPlaying: null,
            isPlaying: false,
            currentTime: 0,
            totalDurationSeconds: 0,
            volume: 80,

            programs: [
                {
                    id: 1,
                    title: "Noticiero SMG",
                    subtitle: "Informativo Escolar",
                    category: "NOTICIAS",
                    description: "Tu fuente confiable de información escolar. Mantente al día con los eventos, logros y noticias más relevantes de nuestra institución.",
                    fullDescription: "El Noticiero SMG es nuestro programa insignia de información escolar, donde los estudiantes se convierten en periodistas y presentadores para mantener informada a toda la comunidad educativa. Con secciones de noticias locales, eventos académicos, logros estudiantiles y entrevistas exclusivas, este programa refleja el pulso diario de nuestra institución. Cada emisión es cuidadosamente investigada y producida por nuestro equipo de comunicaciones estudiantil.",
                    icon: "mdi-newspaper",
                    color: "blue",
                    gradient: "linear-gradient(135deg, #1e3c72 0%, #2a5298 100%)",
                    duration: "6 min",
                    hosts: "4 locutores",
                    date: "marzo 2025",
                    format: "MP3 - 6.509KB  ",
                    audioUrl: "/audios/noticiero smg.mp3",
                    features: ["Noticias", "Entrevistas", "Eventos", "Logros"],
                    team: [
                        { name: "Jander Ensuncho", role: "Presentador Principal" },
                        { name: "Yuliana Otero", role: "Profesora esntrevistada" },
                        { name: "Pedro Romero", role: "Sección sana convivencia" },
                        { name: "Carlos Morales", role: "Deportes" },
                        { name: "Jesus Gonzalez", role: "Editor de audio y creador del jingle" },
                        { name: "Yeison Morelo", role: "Editor de audio" },
                    ],
                    tools: ["Audacity", "Grabadora Digital"],
                    segments: [
                        { time: "00:00", name: "Introducción", description: "Presentación del noticiero y titulares" },
                        { time: "01:00", name: "Noticia Ambiental", description: "¿Sabias que los recursos no estan siendo correctamente depositados?" },
                        { time: "02:11", name: "Noticia de convivencia", description: "La buena convivencia mejora el rendimiento escolar" },
                        { time: "03:20", name: "Anuncio", description: "Acercate al psicologo escolar" },
                        { time: "03:44", name: "Deportes", description: "Las leonas de maria goretti conquistan el intercolegial de voleibol" }
                    ]
                },
                {
                    id: 2,
                    title: "Ecos del Último Código",
                    subtitle: "Radionovela Original",
                    category: "DRAMA",
                    description: "Una emocionante radionovela que mezcla misterio, tecnología y aventura. Sumérgete en una historia original creada por nuestros estudiantes.",
                    fullDescription: "Ecos del Último Código es una radionovela original que transporta a los oyentes a un mundo donde la tecnología y el misterio se entrelazan. Ambientada en un futuro cercano, la historia sigue a un grupo de jóvenes programadores que descubren un código misterioso que podría cambiar el mundo. Con efectos sonoros inmersivos, música original y actuaciones de voz convincentes, esta producción demuestra el talento narrativo y técnico de nuestros estudiantes. Cada episodio está cargado de suspense, drama y elementos de ciencia ficción que mantienen al oyente en vilo.",
                    icon: "mdi-drama-masks",
                    color: "purple",
                    gradient: "linear-gradient(135deg, #667eea 0%, #764ba2 100%)",
                    duration: "5 min",
                    hosts: "6 actores",
                    date: "mayo 2025",
                    format: "MP3 - 6.543kbps",
                    audioUrl: "/audios/Ecos del ultimo codigo.mp3",
                    features: ["Drama", "Ciencia Ficción", "Efectos Sonoros", "Música Original"],
                    team: [
                        { name: "Yuliana Otero", role: "Protagonista - Sofia" },
                        { name: "Pedro Romero", role: "Protagonista - Iván" },
                        { name: "Carlos Morales", role: "Voz encriptada - Elias" },
                        { name: "Yeison Morelo", role: "Narrador" },
                        { name: "Jander Ensuncho", role: "Asistente en cabina" },
                        { name: "Jesus Gonzalez", role: "Director de audio y de edición" }
                    ],
                    tools: ["Audacity", "Adobe Audition", "Efectos de Sonido Digitales","Cabina de grabación Universidad de Cordoba"],
                    segments: [
                        { time: "00:00", name: "Escena 1", description: "Inicio del eco" },
                        { time: "02:17", name: "Escena 2", description: "El eco del pasado" },
                        { time: "03:50", name: "Escena 3", description: "Transferencia" },
                    ]
                },
                {
                    id: 3,
                    title: "Entre Voces",
                    subtitle: "Programa de Talentos",
                    category: "ENTRETENIMIENTO",
                    description: "Celebramos los talentos de nuestra comunidad estudiantil+en un programa lleno de creatividad y diversión.",
                    fullDescription: "Entre Voces es nuestro programa de entretenimiento donde brillan los talentos ocultos de nuestra comunidad educativa. Este programa es una celebración de la creatividad estudiantil. Cada emisión presenta una cuidadosa selección de participantes que han sido elegidos por su originalidad, talento y capacidad de conectar con la audiencia. El programa no solo entretiene, sino que también inspira a otros estudiantes a explorar y compartir sus propios talentos.",
                    icon: "mdi-star",
                    color: "orange",
                    gradient: "linear-gradient(135deg, #f093fb 0%, #f5576c 100%)",
                    duration: "8 min",
                    hosts: "1 presentador, 3 talentos",
                    date: "Diciembre 2024",
                    format: "MP3 - 9.741KB",
                    audioUrl: "/audios/entre voces.mp3",
                    features: ["Música", "Poesía", "Comedy", "Entrevistas"],
                    team: [
                        { name: "Yeison Morelo", role: "Presentador" },
                        { name: "Carlos Morales", role: "JAY-T" },
                        { name: "Jander Ensuncho", role: "Daniel Velez" },
                        { name: "Jesus Gonzalez", role: "Sebastian Cruz" },
                        { name: "Yuliana Otero", role: "Editor Musical" },
                        { name: "Pedro Romero", role: "Productor Ejecutivo" }
                    ],
                    tools: ["Cubase", "Adobe Audition", "Micrófonos Dinámicos", "Mesa de Mezclas"],
                    segments: [
                        { time: "00:00", name: "Apertura Musical", description: "Tema principal y presentación" },
                        { time: "00:50", name: "Primer Talento", description: "Performance musical de JAY-T" },
                        { time: "03:00", name: "Segundo talento", description: "Presentación por parte de Daniel Velez" },
                        { time: "05:40", name: "Tercer talento", description: "Interpretacion de Sebastian Cruz" },
                        { time: "07:40", name: "Despedida", description: "Despedida del programa" },
                    ]
                }
            ]
        };
    },

    computed: {
        totalPrograms() {
            return this.programs.length;
        },

        totalDuration() {
            return this.programs.reduce((total, program) => {
                const duration = parseInt(program.duration.replace(' min', ''));
                return total + duration;
            }, 0);
        },

        totalListeners() {
            return "500+";
        }
    },

    methods: {
        scrollToPrograms() {
            this.$refs.programsSection.scrollIntoView({ behavior: 'smooth' });
        },

        selectProgram(program) {
            this.selectedProgram = program;
        },

        showProgramDetails(program) {
            this.selectedProgram = program;
            this.detailsDialog = true;
        },

        togglePlayback(program) {
            if (this.currentlyPlaying === program.id) {
                this.currentlyPlaying = null;
                this.selectedAudio = null;
                this.isPlaying = false;
                if (this.$refs.audioPlayer) {
                    this.$refs.audioPlayer.pause();
                }
            } else {
                this.currentlyPlaying = program.id;
                this.selectedAudio = program;
                this.isPlaying = false;
                this.$nextTick(() => {
                    if (this.$refs.audioPlayer) {
                        this.$refs.audioPlayer.load();
                    }
                });
            }
        },

        toggleMainPlayback() {
            if (this.$refs.audioPlayer) {
                if (this.isPlaying) {
                    this.$refs.audioPlayer.pause();
                    this.isPlaying = false;
                } else {
                    this.$refs.audioPlayer.play();
                    this.isPlaying = true;
                }
            }
        },

        updateProgress() {
            if (this.$refs.audioPlayer) {
                this.currentTime = this.$refs.audioPlayer.currentTime;
            }
        },

        setDuration() {
            if (this.$refs.audioPlayer) {
                this.totalDurationSeconds = this.$refs.audioPlayer.duration;
            }
        },

        seekTo(time) {
            if (this.$refs.audioPlayer) {
                this.$refs.audioPlayer.currentTime = time;
            }
        },

        setVolume(volume) {
            if (this.$refs.audioPlayer) {
                this.$refs.audioPlayer.volume = volume / 100;
            }
        },

        skipForward() {
            if (this.$refs.audioPlayer) {
                this.$refs.audioPlayer.currentTime += 10;
            }
        },

        skipBackward() {
            if (this.$refs.audioPlayer) {
                this.$refs.audioPlayer.currentTime -= 10;
            }
        },

        audioEnded() {
            this.isPlaying = false;
            this.currentTime = 0;
        },

        closePlayer() {
            this.selectedAudio = null;
            this.currentlyPlaying = null;
            this.isPlaying = false;
            if (this.$refs.audioPlayer) {
                this.$refs.audioPlayer.pause();
            }
        },

        formatTime(seconds) {
            if (!seconds || isNaN(seconds)) return '00:00';
            const mins = Math.floor(seconds / 60);
            const secs = Math.floor(seconds % 60);
            return `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
        }
    },

    mounted() {
        this.$nextTick(() => {
            if (this.$refs.audioPlayer) {
                this.$refs.audioPlayer.volume = this.volume / 100;
            }
        });
    }
};
</script>

<style scoped>
.programas-page {
    min-height: 100vh;
    background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
}

/* Hero Section */
.hero-section {
    position: relative;
    padding: 100px 0;
    background: linear-gradient(135deg, #1b5e20 0%, #2e7d32 50%, #388e3c 100%);
    color: white;
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
    width: 200px;
    height: 200px;
}

.wave {
    position: absolute;
    border: 2px solid rgba(255, 255, 255, 0.1);
    border-radius: 50%;
    animation: wave-pulse 3s ease-in-out infinite;
}

.wave-1 { 
    width: 50px; 
    height: 50px; 
    top: 75px; 
    left: 75px; 
    animation-delay: 0s; 
}

.wave-2 { 
    width: 100px; 
    height: 100px; 
    top: 50px; 
    left: 50px; 
    animation-delay: 0.5s; 
}

.wave-3 { 
    width: 150px; 
    height: 150px; 
    top: 25px; 
    left: 25px; 
    animation-delay: 1s; 
}

.wave-4 { 
    width: 200px; 
    height: 200px; 
    top: 0; 
    left: 0; 
    animation-delay: 1.5s; 
}

@keyframes wave-pulse {
    0%, 100% {
        transform: scale(1);
        opacity: 0.3;
    }
    50% {
        transform: scale(1.1);
        opacity: 0.8;
    }
}

.floating-notes {
    position: absolute;
    width: 100%;
    height: 100%;
    pointer-events: none;
}

.note {
    position: absolute;
    color: rgba(255, 255, 255, 0.2);
    font-size: 24px;
    animation: float-note 6s ease-in-out infinite;
}

.note-1 { top: 20%; left: 10%; animation-delay: 0s; }
.note-2 { top: 30%; right: 15%; animation-delay: 1s; }
.note-3 { bottom: 30%; left: 20%; animation-delay: 2s; }
.note-4 { bottom: 20%; right: 10%; animation-delay: 3s; }
.note-5 { top: 50%; left: 80%; animation-delay: 4s; }

@keyframes float-note {
    0%, 100% {
        transform: translateY(0px) rotate(0deg);
        opacity: 0.2;
    }
    50% {
        transform: translateY(-20px) rotate(180deg);
        opacity: 0.6;
    }
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
    gap: 8px;
    background: rgba(255, 255, 255, 0.1);
    padding: 8px 16px;
    border-radius: 20px;
    margin-bottom: 20px;
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
}

.radio-icon {
    animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.1); }
}

.hero-title {
    font-size: 3.5rem;
    font-weight: 700;
    margin-bottom: 20px;
    line-height: 1.2;
}

.title-highlight {
    background: linear-gradient(45deg, #81c784, #a5d6a7);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    position: relative;
}

.hero-description {
    font-size: 1.2rem;
    margin-bottom: 40px;
    opacity: 0.9;
    line-height: 1.6;
}

.hero-stats {
    display: flex;
    justify-content: center;
    gap: 40px;
    margin-bottom: 40px;
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
    font-size: 0.9rem;
    opacity: 0.8;
    text-transform: uppercase;
    letter-spacing: 1px;
}

.explore-btn {
    margin-top: 20px;
    padding: 15px 30px !important;
    font-size: 1.1rem;
    font-weight: 600;
    border-radius: 30px;
    transition: all 0.3s ease;
}

.explore-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
}

/* Programs Section */
.programs-section {
    padding: 80px 0;
    background: #f8f9fa;
}

.section-header {
    text-align: center;
    margin-bottom: 60px;
}

.section-icon {
    font-size: 3rem;
    color: #2e7d32;
    margin-bottom: 20px;
}

.section-title {
    font-size: 2.5rem;
    font-weight: 700;
    color: #1b5e20;
    margin-bottom: 15px;
}

.section-description {
    font-size: 1.1rem;
    color: #666;
    max-width: 600px;
    margin: 0 auto;
}

.programs-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
    gap: 30px;
    margin-top: 40px;
}

.program-card {
    position: relative;
    border-radius: 20px;
    overflow: hidden;
    transition: all 0.3s ease;
    cursor: pointer;
    background: white;
}

.program-card:hover {
    transform: translateY(-10px);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
}

.card-header {
    position: relative;
    padding: 30px;
    color: white;
    overflow: hidden;
}

.header-pattern {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-image: radial-gradient(circle at 50% 50%, rgba(255, 255, 255, 0.1) 0%, transparent 70%);
}

.program-icon {
    position: relative;
    z-index: 2;
    margin-bottom: 15px;
}

.program-category {
    position: relative;
    z-index: 2;
    font-size: 0.9rem;
    font-weight: 600;
    letter-spacing: 2px;
    opacity: 0.9;
}

.program-content {
    padding: 30px;
}

.program-title-section {
    margin-bottom: 20px;
}

.program-title {
    font-size: 1.8rem;
    font-weight: 700;
    color: #1b5e20;
    margin-bottom: 8px;
}

.program-subtitle {
    font-size: 1rem;
    color: #666;
    font-weight: 500;
}

.program-description {
    color: #555;
    line-height: 1.6;
    margin-bottom: 25px;
}

.program-details {
    display: flex;
    flex-wrap: wrap;
    gap: 15px;
    margin-bottom: 20px;
}

.detail-item {
    display: flex;
    align-items: center;
    gap: 6px;
    font-size: 0.9rem;
    color: #666;
}

.program-features {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 25px;
}

.feature-chip {
    font-size: 0.8rem;
}

.program-actions {
    display: flex;
    gap: 15px;
    align-items: center;
}

.play-btn {
    flex: 1;
    border-radius: 25px;
    font-weight: 600;
}

/* Featured Section */
.featured-section {
    padding: 80px 0;
    background: linear-gradient(135deg, #1b5e20 0%, #2e7d32 100%);
    color: white;
}

.featured-content {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 60px;
    align-items: center;
}

.featured-title {
    font-size: 2.5rem;
    font-weight: 700;
    margin-bottom: 20px;
}

.featured-description {
    font-size: 1.1rem;
    line-height: 1.7;
    margin-bottom: 40px;
    opacity: 0.9;
}

.featured-highlights {
    display: flex;
    flex-direction: column;
    gap: 25px;
}

.highlight-item {
    display: flex;
    align-items: flex-start;
    gap: 20px;
}

.highlight-item h4 {
    font-size: 1.2rem;
    font-weight: 600;
    margin-bottom: 5px;
}

.highlight-item p {
    opacity: 0.8;
    line-height: 1.5;
}

.featured-visual {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
}

.studio-illustration {
    position: relative;
    width: 300px;
    height: 300px;
}

.studio-circle {
    position: absolute;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    backdrop-filter: blur(10px);
    border: 2px solid rgba(255, 255, 255, 0.2);
    animation: float 6s ease-in-out infinite;
}

.main-circle {
    width: 150px;
    height: 150px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: rgba(255, 255, 255, 0.2);
}

.circle-1 {
    width: 80px;
    height: 80px;
    top: 10%;
    left: 10%;
    animation-delay: 0s;
}

.circle-2 {
    width: 80px;
    height: 80px;
    top: 10%;
    right: 10%;
    animation-delay: 2s;
}

.circle-3 {
    width: 80px;
    height: 80px;
    bottom: 10%;
    left: 50%;
    transform: translateX(-50%);
    animation-delay: 4s;
}

@keyframes float {
    0%, 100% {
        transform: translateY(0px);
    }
    50% {
        transform: translateY(-10px);
    }
}

/* Audio Player Section */
.player-section {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 1000;
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(10px);
    border-top: 1px solid rgba(0, 0, 0, 0.1);
}

.audio-player {
    background: white;
    border-radius: 15px 15px 0 0;
    overflow: hidden;
}

.player-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 15px 20px;
    background: #f5f5f5;
    border-bottom: 1px solid #e0e0e0;
}

.now-playing {
    display: flex;
    align-items: center;
    gap: 10px;
    font-weight: 600;
    color: #2e7d32;
}

.pulse-icon {
    animation: pulse 2s ease-in-out infinite;
}

.player-content {
    padding: 20px;
}

.player-info {
    text-align: center;
    margin-bottom: 20px;
}

.player-title {
    font-size: 1.3rem;
    font-weight: 700;
    color: #1b5e20;
    margin-bottom: 5px;
}

.player-subtitle {
    color: #666;
    font-size: 0.9rem;
}

.player-controls {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
}

.control-buttons {
    display: flex;
    align-items: center;
    gap: 20px;
}

.play-button {
    box-shadow: 0 4px 15px rgba(46, 125, 50, 0.3);
}

.progress-section {
    display: flex;
    align-items: center;
    gap: 15px;
    width: 100%;
    max-width: 600px;
}

.progress-slider {
    flex: 1;
}

.time-display {
    font-size: 0.9rem;
    color: #666;
    min-width: 45px;
    text-align: center;
}

.volume-section {
    display: flex;
    align-items: center;
    gap: 10px;
    width: 200px;
}

.volume-slider {
    flex: 1;
}

/* Program Details Dialog */
.program-details-dialog {
    max-height: 90vh;
    overflow-y: auto;
}

.dialog-header {
    display: flex;
    align-items: center;
    padding: 30px;
    color: white;
    position: relative;
    overflow: hidden;
}

.dialog-header::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: radial-gradient(circle at 30% 30%, rgba(255, 255, 255, 0.1) 0%, transparent 70%);
}

.dialog-icon {
    position: relative;
    z-index: 2;
    margin-right: 20px;
}

.dialog-info {
    position: relative;
    z-index: 2;
    flex: 1;
}

.dialog-title {
    font-size: 2rem;
    font-weight: 700;
    margin-bottom: 5px;
}

.dialog-subtitle {
    font-size: 1.1rem;
    opacity: 0.9;
}

.dialog-content {
    padding: 30px;
}

.dialog-section {
    margin-bottom: 30px;
}

.section-subtitle {
    font-size: 1.3rem;
    font-weight: 600;
    color: #1b5e20;
    margin-bottom: 15px;
    display: flex;
    align-items: center;
    gap: 10px;
}

.program-full-description {
    line-height: 1.7;
    color: #555;
    font-size: 1rem;
}

.team-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
}

.team-member {
    display: flex;
    align-items: center;
    gap: 15px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 10px;
    transition: all 0.3s ease;
}

.team-member:hover {
    background: #e8f5e8;
    transform: translateY(-2px);
}

.member-info {
    flex: 1;
}

.member-name {
    font-size: 1rem;
    font-weight: 600;
    color: #1b5e20;
    margin-bottom: 3px;
}

.member-role {
    font-size: 0.9rem;
    color: #666;
}

.technical-details {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 15px;
}

.tech-item {
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    border-left: 4px solid #2e7d32;
}

.tech-item strong {
    color: #1b5e20;
}

.segments-list {
    display: flex;
    flex-direction: column;
    gap: 15px;
}

.segment-item {
    display: flex;
    gap: 20px;
    padding: 20px;
    background: #f8f9fa;
    border-radius: 10px;
    border-left: 4px solid #2e7d32;
    transition: all 0.3s ease;
}

.segment-item:hover {
    background: #e8f5e8;
    transform: translateX(5px);
}

.segment-time {
    font-family: 'Courier New', monospace;
    font-weight: 700;
    color: #2e7d32;
    min-width: 60px;
    background: white;
    padding: 5px 10px;
    border-radius: 5px;
    text-align: center;
    font-size: 0.9rem;
}

.segment-info {
    flex: 1;
}

.segment-name {
    font-size: 1.1rem;
    font-weight: 600;
    color: #1b5e20;
    margin-bottom: 5px;
}

.segment-description {
    color: #666;
    line-height: 1.5;
}

/* Responsive Design */
@media (max-width: 768px) {
    .hero-title {
        font-size: 2.5rem;
    }
    
    .hero-stats {
        flex-direction: column;
        gap: 20px;
    }
    
    .programs-grid {
        grid-template-columns: 1fr;
        gap: 20px;
    }
    
    .featured-content {
        grid-template-columns: 1fr;
        gap: 40px;
        text-align: center;
    }
    
    .program-actions {
        flex-direction: column;
        gap: 10px;
    }
    
    .control-buttons {
        gap: 15px;
    }
    
    .progress-section {
        flex-direction: column;
        gap: 10px;
    }
    
    .time-display {
        min-width: auto;
    }
    
    .team-list {
        grid-template-columns: 1fr;
    }
    
    .technical-details {
        grid-template-columns: 1fr;
    }
    
    .segment-item {
        flex-direction: column;
        gap: 10px;
    }
    
    .segment-time {
        align-self: flex-start;
    }
}

@media (max-width: 480px) {
    .hero-section {
        padding: 60px 0;
    }
    
    .hero-title {
        font-size: 2rem;
    }
    
    .programs-section {
        padding: 60px 0;
    }
    
    .program-card {
        margin: 0 10px;
    }
    
    .dialog-header {
        flex-direction: column;
        text-align: center;
        gap: 15px;
    }
    
    .dialog-icon {
        margin-right: 0;
    }
}
</style>
    