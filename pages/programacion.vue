<template>
    <div class="programacion-page">
        <!-- Hero Section -->
        <section class="hero-section">
            <div class="hero-background">
                <div class="floating-icons">
                    <div class="floating-icon icon-1">🎵</div>
                    <div class="floating-icon icon-2">📻</div>
                    <div class="floating-icon icon-3">🎤</div>
                    <div class="floating-icon icon-4">🌟</div>
                    <div class="floating-icon icon-5">📰</div>
                    <div class="floating-icon icon-6">🎨</div>
                </div>
            </div>

            <v-container>
                <div class="hero-content">
                    <div class="hero-badge">
                        <v-icon class="pulse-icon">mdi-radio</v-icon>
                        <span>PROGRAMACIÓN EN VIVO</span>
                    </div>

                    <h1 class="hero-title">
                        Nuestra Programación
                        <span class="title-highlight">Semanal</span>
                    </h1>

                    <p class="hero-description">
                        Descubre todos nuestros programas educativos, culturales y de
                        entretenimiento. Una programación diseñada especialmente para
                        nuestra comunidad estudiantil.
                    </p>

                    <div class="current-show-card" v-if="currentShow">
                        <div class="live-indicator">
                            <div class="pulse-dot"></div>
                            <span class="live-text">EN VIVO AHORA</span>
                        </div>
                        <div class="show-info">
                            <h3 class="show-name">{{ currentShow.title }}</h3>
                            <p class="show-time">{{ currentShow.time }}</p>
                            <p class="show-description">{{ currentShow.description }}</p>
                            <div class="show-category">{{ currentShow.category }}</div>
                        </div>
                    </div>

                    <div class="current-show-card off-air" v-else>
                        <div class="live-indicator">
                            <div class="off-air-dot"></div>
                            <span class="off-air-text">FUERA DEL AIRE</span>
                        </div>
                        <div class="show-info">
                            <h3 class="show-name">Sin transmisión</h3>
                            <p class="show-time">{{ getCurrentTime() }}</p>
                            <p class="show-description">
                                No hay programación en este horario.
                                Próximo programa: {{ nextShow ? nextShow.title + ' - ' + nextShow.time : 'Por definir'
                                }}
                            </p>
                        </div>
                    </div>
                </div>
            </v-container>
        </section>

        <!-- Programming Schedule -->
        <section class="schedule-section">
            <v-container>
                <div class="section-header">
                    <v-icon class="section-icon">mdi-calendar-clock</v-icon>
                    <h2 class="section-title">Horario Semanal</h2>
                    <p class="section-description">
                        Nuestra programación está diseñada para acompañarte durante toda la
                        jornada escolar
                    </p>
                </div>

                <!-- Schedule Table -->
                <div class="schedule-container">
                    <v-card class="schedule-card" elevation="0">
                        <div class="schedule-header">
                            <div class="time-column header-cell">
                                <v-icon>mdi-clock-outline</v-icon>
                                <span>Horario</span>
                            </div>
                            <div v-for="day in weekDays" :key="day" class="day-column header-cell">
                                <v-icon>{{ getDayIcon(day) }}</v-icon>
                                <span>{{ day }}</span>
                            </div>
                        </div>

                        <div class="schedule-body">
                            <div v-for="slot in timeSlots" :key="slot.time" class="time-row">
                                <div class="time-column time-cell">
                                    <span class="time-text">{{ slot.time }}</span>
                                </div>

                                <div v-for="(day, index) in weekDays" :key="day" class="day-column program-cell">
                                    <div v-if="slot.programs[index]" class="program-card"
                                        :class="getProgramClass(slot.programs[index].category)">
                                        <div class="program-icon">
                                            {{ slot.programs[index].icon }}
                                        </div>
                                        <div class="program-content">
                                            <h4 class="program-title">
                                                {{ slot.programs[index].title }}
                                            </h4>
                                            <p class="program-category">
                                                {{ slot.programs[index].category }}
                                            </p>
                                            <p class="program-description">
                                                {{ slot.programs[index].description }}
                                            </p>
                                        </div>
                                        <div class="program-duration">
                                            {{ slot.programs[index].duration }}
                                        </div>
                                        
                                        <!-- Audio Player Button -->
                                        <div class="audio-player" v-if="slot.programs[index].audioFile">
                                            <v-btn 
                                                :icon="currentPlayingAudio === slot.programs[index].audioFile && isPlaying ? 'mdi-pause' : 'mdi-play'"
                                                size="small"
                                                color="primary"
                                                variant="elevated"
                                                class="audio-btn"
                                                @click="toggleAudio(slot.programs[index].audioFile)"
                                            ></v-btn>
                                        </div>
                                    </div>
                                    <div v-else class="empty-slot">
                                        <v-icon color="grey lighten-2">mdi-music-note-off</v-icon>
                                        <span>Descanso</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </v-card>
                </div>

                <!-- Program Categories -->
                <div class="categories-section">
                    <h3 class="categories-title">Categorías de Programas</h3>
                    <div class="categories-grid">
                        <v-card v-for="category in programCategories" :key="category.name" class="category-card"
                            :class="category.class" elevation="2">
                            <div class="category-icon">{{ category.icon }}</div>
                            <h4 class="category-name">{{ category.name }}</h4>
                            <p class="category-description">{{ category.description }}</p>
                            <div class="category-count">{{ category.count }} programas</div>
                        </v-card>
                    </div>
                </div>

                <!-- Special Programs -->
                <div class="special-programs-section">
                    <h3 class="section-subtitle">Programas Especiales</h3>
                    <div class="special-programs-grid">
                        <v-card v-for="special in specialPrograms" :key="special.name" class="special-program-card"
                            elevation="4">
                            <div class="special-program-header" :style="{ background: special.gradient }">
                                <div class="special-icon">{{ special.icon }}</div>
                                <div class="special-badge">{{ special.badge }}</div>
                            </div>

                            <div class="special-program-content">
                                <h4 class="special-title">{{ special.name }}</h4>
                                <p class="special-description">{{ special.description }}</p>
                                <div class="special-details">
                                    <div class="special-time">
                                        <v-icon size="small">mdi-clock</v-icon>
                                        {{ special.time }}
                                    </div>
                                    <div class="special-day">
                                        <v-icon size="small">mdi-calendar</v-icon>
                                        {{ special.day }}
                                    </div>
                                </div>
                            </div>
                        </v-card>
                    </div>
                </div>

                <!-- Participation Section -->
                <div class="participation-section">
                    <v-card class="participation-card" color="green" dark elevation="8">
                        <v-card-text>
                            <div class="participation-content">
                                <div class="participation-text">
                                    <v-icon size="48" class="participation-icon">mdi-microphone</v-icon>
                                    <h3 class="participation-title">
                                        ¡Participa en Nuestros Programas!
                                    </h3>
                                    <p class="participation-description">
                                        ¿Tienes una historia que contar? ¿Una noticia que compartir?
                                        ¡Únete a nosotros y forma parte de la voz estudiantil!
                                    </p>
                                </div>
                                <div class="participation-actions">
                                    <v-btn size="large" variant="outlined" color="white" prepend-icon="mdi-phone"
                                        class="participation-btn">
                                        Contáctanos
                                    </v-btn>
                                    <v-btn size="large" variant="elevated" color="white" text-color="Primary"
                                        prepend-icon="mdi-email" class="participation-btn">
                                        Envía tu Propuesta
                                    </v-btn>
                                </div>
                            </div>
                        </v-card-text>
                    </v-card>
                </div>
            </v-container>
        </section>

        <!-- Audio Element -->
        <audio ref="audioPlayer" @ended="onAudioEnded" @play="onAudioPlay" @pause="onAudioPause"></audio>
    </div>
</template>

<script>
export default {
    name: "ProgramacionPage",

    data() {
        return {
            currentTime: new Date(),
            currentShow: null,
            nextShow: null,
            timeInterval: null,
            currentPlayingAudio: null,
            isPlaying: false,

            weekDays: ["Lunes", "Martes", "Miércoles", "Jueves", "Viernes"],

            timeSlots: [
                {
                    time: "8:00 - 9:00 AM",
                    startHour: 8,
                    startMinute: 0,
                    endHour: 9,
                    endMinute: 0,
                    programs: [
                        {
                            title: "Noticias gorettianas",
                            category: "Informativo",
                            description: "Noticias importantes de la institución",
                            icon: "📰",
                            duration: "60 min",
                            audioFile: "noticiero smg.mp3",
                        },
                        {
                            title: "Música y Cultura",
                            category: "Cultural",
                            description: "Lo mejor de la música y expresiones culturales",
                            icon: "🎵",
                            duration: "60 min",
                            audioFile: "musicaycultura.mp3",
                        },
                        {
                            title: "Entrevistas Especiales",
                            category: "Entrevistas",
                            description: "Conversaciones con invitados especiales",
                            icon: "🎤",
                            duration: "60 min",
                            audioFile: "entrevistasespeciales.mp3",
                        },
                        {
                            title: "Ciencia y Tecnología",
                            category: "Educativo",
                            description: "Descubrimientos científicos y avances tecnológicos",
                            icon: "🔬",
                            duration: "60 min",
                            audioFile: "cienciaytecnologia.mp3",
                        },
                        {
                            title: "Deportes y Recreación",
                            category: "Deportivo",
                            description: "Noticias deportivas y actividades recreativas",
                            icon: "⚽",
                            duration: "60 min",
                            audioFile: "deportesyrecreacion.mp3",
                        },
                    ],
                },
                {
                    time: "9:00 - 10:00 AM",
                    startHour: 9,
                    startMinute: 0,
                    endHour: 10,
                    endMinute: 0,
                    programs: [
                        {
                            title: "Historia y Tradición",
                            category: "Educativo",
                            description: "Explorando nuestras raíces históricas",
                            icon: "📚",
                            duration: "60 min",
                            audioFile: "historiaytradicion.mp3",
                        },
                        {
                            title: "Literatura al Aire",
                            category: "Cultural",
                            description: "Poesía, cuentos y literatura estudiantil",
                            icon: "📖",
                            duration: "60 min",
                            audioFile: "literaturaalaire.mp3",
                        },
                        {
                            title: "Debates Estudiantiles",
                            category: "Participativo",
                            description: "Discusiones sobre temas de interés estudiantil",
                            icon: "💭",
                            duration: "60 min",
                            audioFile: "debatesestudiantiles.mp3",
                        },
                        {
                            title: "Arte y Creatividad",
                            category: "Cultural",
                            description: "Showcases de talentos artísticos estudiantiles",
                            icon: "🎨",
                            duration: "60 min",
                            audioFile: "arteycreatividadv.mp3",
                        },
                        {
                            title: "Resumen Semanal",
                            category: "Informativo",
                            description: "Recapitulación de eventos de la semana",
                            icon: "📝",
                            duration: "60 min",
                            audioFile: "resumensemanal.mp3",
                        },
                    ],
                },
                {
                    time: "12:00 - 12:30 PM",
                    startHour: 12,
                    startMinute: 0,
                    endHour: 12,
                    endMinute: 30,
                    programs: [
                        {
                            title: "Música del Almuerzo",
                            category: "Musical",
                            description: "Ritmos culturales para acompañar tu almuerzo",
                            icon: "🎶",
                            duration: "30 min",
                            audioFile: "musicadelalmuerzo.mp3",
                        },
                        {
                            title: "Música del Almuerzo",
                            category: "Musical",
                            description: "Ritmos culturales para acompañar tu almuerzo",
                            icon: "🎶",
                            duration: "30 min",
                            audioFile: "musicadelalmuerzo.mp3",
                        },
                        {
                            title: "Música del Almuerzo",
                            category: "Musical",
                            description: "Ritmos culturales para acompañar tu almuerzo",
                            icon: "🎶",
                            duration: "30 min",
                            audioFile: "musicadelalmuerzo.mp3",
                        },
                        {
                            title: "Música del Almuerzo",
                            category: "Musical",
                            description: "Ritmos culturales para acompañar tu almuerzo",
                            icon: "🎶",
                            duration: "30 min",
                            audioFile: "musicadelalmuerzo.mp3",
                        },
                        {
                            title: "Música del Almuerzo",
                            category: "Musical",
                            description: "Ritmos culturales para acompañar tu almuerzo",
                            icon: "🎶",
                            duration: "30 min",
                            audioFile: "musicadelalmuerzo.mp3",
                        },
                    ],
                },
                {
                    time: "2:00 - 3:00 PM",
                    startHour: 14,
                    startMinute: 0,
                    endHour: 15,
                    endMinute: 0,
                    programs: [
                        {
                            title: "Reflexiones y Valores",
                            category: "Formativo",
                            description: "Momentos de reflexión sobre valores cristianos",
                            icon: "🙏",
                            duration: "60 min",
                            audioFile: "reflexionesyvalores.mp3",
                        },
                        {
                            title: "Ecología y Ambiente",
                            category: "Ambiental",
                            description: "Conciencia ambiental y cuidado del planeta",
                            icon: "🌍",
                            duration: "60 min",
                            audioFile: "ecologiayambiente.mp3",
                        },
                        {
                            title: "Ecos del último código",
                            category: "Entretenimiento",
                            description: "Radionovela de suspenso (programa grabado)",
                            icon: "🎭",
                            duration: "60 min",
                            audioFile: "ecos del ultimo codigo.mp3",
                        },
                        {
                            title: "Logros Institucionales",
                            category: "Institucional",
                            description: "Reconocimientos y logros de la comunidad",
                            icon: "🏆",
                            duration: "60 min",
                            audioFile: "logrosinstitucionales.mp3",
                        },
                        {
                            title: "Entre voces",
                            category: "Entretenimiento",
                            description: "Programa de entretenimiento de concurso de canto (programa grabado)",
                            icon: "🎤",
                            duration: "60 min",
                            audioFile: "entre voces.mp3",
                        },
                    ],
                },
            ],

            programCategories: [
                {
                    name: "Informativos",
                    description: "Noticias y comunicados importantes",
                    icon: "📰",
                    count: 3,
                    class: "category-informativo",
                },
                {
                    name: "Culturales",
                    description: "Música, arte y expresiones culturales",
                    icon: "🎭",
                    count: 5,
                    class: "category-cultural",
                },
                {
                    name: "Educativos",
                    description: "Contenido formativo y académico",
                    icon: "📚",
                    count: 4,
                    class: "category-educativo",
                },
                {
                    name: "Deportivos",
                    description: "Actividades físicas y deportivas",
                    icon: "⚽",
                    count: 2,
                    class: "category-deportivo",
                },
                {
                    name: "Entretenimiento",
                    description: "Programas grabados de concursos y radionovelas",
                    icon: "🎭",
                    count: 2,
                    class: "category-entretenimiento",
                },
                {
                    name: "Formativos",
                    description: "Valores y formación integral",
                    icon: "🙏",
                    count: 2,
                    class: "category-formativo",
                },
                {
                    name: "Musicales",
                    description: "Programas de música para diferentes momentos",
                    icon: "🎶",
                    count: 1,
                    class: "category-musical",
                },
            ],

            specialPrograms: [
                {
                    name: "Festival de Talentos",
                    description:
                        "Evento especial mensual donde los estudiantes muestran sus habilidades artísticas",
                    icon: "🌟",
                    badge: "MENSUAL",
                    time: "2:00 - 4:00 PM",
                    day: "Último viernes",
                    gradient: "linear-gradient(135deg, #667eea 0%, #764ba2 100%)",
                },
                {
                    name: "Mesa Redonda Estudiantil",
                    description:
                        "Debates sobre temas de actualidad con la participación de toda la comunidad",
                    icon: "🗣️",
                    badge: "QUINCENAL",
                    time: "9:00 - 10:30 AM",
                    day: "Cada 15 días",
                    gradient: "linear-gradient(135deg, #f093fb 0%, #f5576c 100%)",
                },
                {
                    name: "Concierto Gorettiano",
                    description:
                        "Presentaciones musicales en vivo de estudiantes y grupos invitados",
                    icon: "🎵",
                    badge: "TRIMESTRAL",
                    time: "10:00 - 12:00 PM",
                    day: "Eventos especiales",
                    gradient: "linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)",
                },
            ],
        };
    },

    mounted() {
        this.updateCurrentShow();
        // Actualizar cada minuto
        this.timeInterval = setInterval(() => {
            this.currentTime = new Date();
            this.updateCurrentShow();
        }, 60000);
    },

    beforeUnmount() {
        if (this.timeInterval) {
            clearInterval(this.timeInterval);
        }
        if (this.$refs.audioPlayer) {
            this.$refs.audioPlayer.pause();
        }
    },

    methods: {
        toggleAudio(audioFile) {
            const audio = this.$refs.audioPlayer;
            
            if (this.currentPlayingAudio === audioFile && this.isPlaying) {
                // Pausar el audio actual
                audio.pause();
            } else {
                // Reproducir nuevo audio o reanudar el pausado
                if (this.currentPlayingAudio !== audioFile) {
                    // Cambiar de audio
                    this.currentPlayingAudio = audioFile;
                    // Ruta corregida
                    audio.src = `./audios/${audioFile}`;
                }
                audio.play().catch(error => {
                    console.error('Error al reproducir audio:', error);
                    // Mensaje de error más informativo
                    alert(`No se pudo reproducir el audio: ${audioFile}. Verifica que el archivo existe en la carpeta audios.`);
                });
            }
        },

        onAudioPlay() {
            this.isPlaying = true;
        },

        onAudioPause() {
            this.isPlaying = false;
        },

        onAudioEnded() {
            this.isPlaying = false;
            this.currentPlayingAudio = null;
        },

        updateCurrentShow() {
            const now = new Date();
            const currentDay = now.getDay(); // 0 = Domingo, 1 = Lunes, etc.
            const currentHour = now.getHours();
            const currentMinute = now.getMinutes();

            // Solo mostrar programas de lunes a viernes (1-5)
            if (currentDay >= 1 && currentDay <= 5) {
                const dayIndex = currentDay - 1; // Convertir a índice 0-4 para nuestro array

                // Buscar el programa actual
                for (let slot of this.timeSlots) {
                    if (this.isTimeInSlot(currentHour, currentMinute, slot)) {
                        const program = slot.programs[dayIndex];
                        if (program) {
                            this.currentShow = {
                                ...program,
                                time: slot.time
                            };
                            this.findNextShow(dayIndex, slot);
                            return;
                        }
                    }
                }
            }

            // No hay programa en este momento
            this.currentShow = null;
            this.findNextShow(currentDay >= 1 && currentDay <= 5 ? currentDay - 1 : 0);
        },

        isTimeInSlot(hour, minute, slot) {
            const currentMinutes = hour * 60 + minute;
            const startMinutes = slot.startHour * 60 + slot.startMinute;
            const endMinutes = slot.endHour * 60 + slot.endMinute;
            
            return currentMinutes >= startMinutes && currentMinutes < endMinutes;
        },

        findNextShow(currentDayIndex, currentSlot = null) {
            const now = new Date();
            let searchDay = currentDayIndex;
            let searchSlotIndex = currentSlot ? this.timeSlots.indexOf(currentSlot) + 1 : 0;

            // Buscar en el día actual primero
            for (let i = searchSlotIndex; i < this.timeSlots.length; i++) {
                const program = this.timeSlots[i].programs[searchDay];
                if (program) {
                    this.nextShow = {
                        ...program,
                        time: this.timeSlots[i].time,
                        day: this.weekDays[searchDay]
                    };
                    return;
                }
            }

            // Buscar en los siguientes días
            for (let d = 1; d < 5; d++) {
                const nextDay = (searchDay + d) % 5;
                for (let slot of this.timeSlots) {
                    const program = slot.programs[nextDay];
                    if (program) {
                        this.nextShow = {
                            ...program,
                            time: slot.time,
                            day: this.weekDays[nextDay]
                        };
                        return;
                    }
                }
            }

            this.nextShow = null;
        },

        isCurrentProgram(slot, dayIndex) {
            if (!this.currentShow) return false;
            
            const now = new Date();
            const currentDay = now.getDay();
            const currentHour = now.getHours();
            const currentMinute = now.getMinutes();

            // Verificar si es el día correcto (lunes = 1, corresponde a índice 0)
            if (currentDay < 1 || currentDay > 5) return false;
            
            const currentDayIndex = currentDay - 1;
            if (currentDayIndex !== dayIndex) return false;

            // Verificar si es la hora correcta
            return this.isTimeInSlot(currentHour, currentMinute, slot);
        },

        getCurrentTime() {
            return this.currentTime.toLocaleTimeString('es-ES', {
                hour: '2-digit',
                minute: '2-digit',
                hour12: true
            });
        },

        getDayIcon(day) {
            const icons = {
                "Lunes": "mdi-calendar-week-begin",
                "Martes": "mdi-calendar-today",
                "Miércoles": "mdi-calendar-today",
                "Jueves": "mdi-calendar-today",
                "Viernes": "mdi-calendar-week-end",
            };
            return icons[day] || "mdi-calendar";
        },

        getProgramClass(category) {
            return `program-${category.toLowerCase().replace(/\s+/g, "-")}`;
        },
    },
};
</script>

<style scoped>
.programacion-page {
    min-height: 100vh;
    background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
}

/* Hero Section */
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

.icon-1 {
    top: 20%;
    left: 10%;
    animation-delay: 0s;
}

.icon-2 {
    top: 30%;
    right: 15%;
    animation-delay: 1s;
}

.icon-3 {
    bottom: 40%;
    left: 20%;
    animation-delay: 2s;
}

.icon-4 {
    top: 60%;
    right: 25%;
    animation-delay: 3s;
}

.icon-5 {
    bottom: 20%;
    right: 10%;
    animation-delay: 4s;
}

.icon-6 {
    top: 70%;
    left: 30%;
    animation-delay: 5s;
}

@keyframes float {
    0%, 100% {
        transform: translateY(0px) rotate(0deg);
    }
    25% {
        transform: translateY(-20px) rotate(5deg);
    }
    50% {
        transform: translateY(-10px) rotate(-5deg);
    }
    75% {
        transform: translateY(-15px) rotate(3deg);
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
    0%, 100% {
        opacity: 1;
        transform: scale(1);
    }
    50% {
        opacity: 0.7;
        transform: scale(1.1);
    }
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

.current-show-card {
    background: rgba(255, 255, 255, 0.1);
    padding: 25px;
    border-radius: 20px;
    backdrop-filter: blur(15px);
    border: 1px solid rgba(255, 255, 255, 0.2);
    margin-top: 30px;
    text-align: left;
}

.current-show-card.off-air {
    background: rgba(158, 158, 158, 0.1);
    border: 1px solid rgba(158, 158, 158, 0.2);
}

.live-indicator {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 15px;
}

.pulse-dot {
    width: 12px;
    height: 12px;
    background: #4caf50;
    border-radius: 50%;
    animation: pulse-dot 1.5s ease-in-out infinite;
}

.off-air-dot {
    width: 12px;
    height: 12px;
    background: #757575;
    border-radius: 50%;
}

@keyframes pulse-dot {
    0%, 100% {
        opacity: 1;
        transform: scale(1);
    }
    50% {
        opacity: 0.3;
        transform: scale(1.2);
    }
}

.live-text {
    font-weight: 700;
    font-size: 0.9rem;
    letter-spacing: 1px;
    color: #4caf50;
}

.off-air-text {
    font-weight: 700;
    font-size: 0.9rem;
    letter-spacing: 1px;
    color: #757575;
}

.show-info .show-name {
    font-size: 1.5rem;
    font-weight: 600;
    margin-bottom: 5px;
}

.show-info .show-time {
    color: rgba(255, 255, 255, 0.8);
    margin-bottom: 10px;
    font-weight: 500;
}

.show-info .show-description {
    margin-bottom: 15px;
    line-height: 1.5;
}

.show-category {
    display: inline-block;
    background: rgba(255, 255, 255, 0.2);
    padding: 4px 12px;
    border-radius: 15px;
    font-size: 0.85rem;
    font-weight: 500;
}

/* Schedule Section */
.schedule-section {
    padding: 80px 0;
}

.section-header {
    text-align: center;
    margin-bottom: 60px;
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
    font-size: 1.1rem;
    color: #666;
    max-width: 600px;
    margin: 0 auto;
}

.schedule-container {
    margin-bottom: 60px;
}

.schedule-card {
    border-radius: 20px;
    overflow: hidden;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.schedule-header {
    display: grid;
    grid-template-columns: 150px repeat(5, 1fr);
    background: linear-gradient(135deg, #2e7d32, #1b5e20);
    color: white;
}

.header-cell {
    padding: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    font-weight: 600;
    border-right: 1px solid rgba(255, 255, 255, 0.1);
}

.header-cell:last-child {
    border-right: none;
}

.schedule-body {
    background: white;
}

.time-row {
    display: grid;
    grid-template-columns: 150px repeat(5, 1fr);
    border-bottom: 1px solid #e0e0e0;
}

.time-row:last-child {
    border-bottom: none;
}

.time-cell {
    padding: 20px;
    background: #f8f9fa;
    display: flex;
    align-items: center;
    justify-content: center;
    border-right: 1px solid #e0e0e0;
    font-weight: 600;
    color: #2e7d32;
}

.time-text {
    font-size: 0.9rem;
}

.program-cell {
    padding: 15px;
    border-right: 1px solid #e0e0e0;
    position: relative;
}

.program-cell:last-child {
    border-right: none;
}

.program-card {
    position: relative;
    padding: 20px;
    border-radius: 12px;
    height: 100%;
    min-height: 140px;
    display: flex;
    flex-direction: column;
    transition: all 0.3s ease;
    cursor: pointer;
}

.program-card:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.program-icon {
    font-size: 2rem;
    margin-bottom: 10px;
}

.program-content {
    flex: 1;
}

.program-title {
    font-size: 1rem;
    font-weight: 600;
    margin-bottom: 5px;
    line-height: 1.2;
}

.program-category {
    font-size: 0.8rem;
    margin-bottom: 8px;
    opacity: 0.8;
    font-weight: 500;
}

.program-description {
    font-size: 0.85rem;
    line-height: 1.4;
    margin-bottom: 10px;
    opacity: 0.9;
}

.program-duration {
    font-size: 0.75rem;
    font-weight: 600;
    padding: 4px 8px;
    border-radius: 10px;
    background: rgba(255, 255, 255, 0.2);
    align-self: flex-start;
    margin-top: auto;
}

/* Program Categories Styles */
.program-informativo {
    background: linear-gradient(135deg, #1976d2, #1565c0);
    color: white;
}

.program-cultural {
    background: linear-gradient(135deg, #7b1fa2, #6a1b9a);
    color: white;
}

.program-educativo {
    background: linear-gradient(135deg, #388e3c, #2e7d32);
    color: white;
}

.program-deportivo {
    background: linear-gradient(135deg, #f57c00, #ef6c00);
    color: white;
}

.program-entretenimiento {
    background: linear-gradient(135deg, #e91e63, #c2185b);
    color: white;
}

.program-formativo {
    background: linear-gradient(135deg, #5d4037, #4e342e);
    color: white;
}

.program-participativo {
    background: linear-gradient(135deg, #00796b, #00695c);
    color: white;
}

.program-ambiental {
    background: linear-gradient(135deg, #689f38, #558b2f);
    color: white;
}

.program-institucional {
    background: linear-gradient(135deg, #455a64, #37474f);
    color: white;
}

.empty-slot {
    padding: 20px;
    text-align: center;
    color: #bbb;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 8px;
    min-height: 140px;
}

/* Audio Player Styles */
.audio-player {
    position: absolute;
    top: 15px;
    right: 15px;
}

.audio-btn {
    width: 36px !important;
    height: 36px !important;
    min-width: 36px !important;
    background: rgba(255, 255, 255, 0.9) !important;
    color: #2e7d32 !important;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15) !important;
}

.audio-btn:hover {
    background: white !important;
    transform: scale(1.1);
}

/* Lunch Music Section */
.lunch-music-section {
    margin: 60px 0;
}

.lunch-card {
    background: linear-gradient(135deg, #ff9800, #f57c00);
    color: white;
    border-radius: 20px;
    overflow: hidden;
    position: relative;
}

.lunch-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><circle cx="20" cy="20" r="2" fill="rgba(255,255,255,0.1)"/><circle cx="80" cy="40" r="1.5" fill="rgba(255,255,255,0.1)"/><circle cx="40" cy="70" r="1" fill="rgba(255,255,255,0.1)"/></svg>');
    opacity: 0.3;
}

.lunch-header {
    padding: 30px;
    text-align: center;
    position: relative;
    z-index: 1;
}

.lunch-icon {
    font-size: 3rem;
    margin-bottom: 15px;
}

.lunch-title {
    font-size: 2rem;
    font-weight: 700;
    margin-bottom: 10px;
}

.lunch-subtitle {
    font-size: 1.1rem;
    opacity: 0.9;
}

.lunch-content {
    padding: 0 30px 30px;
    text-align: center;
    position: relative;
    z-index: 1;
}

.lunch-description {
    font-size: 1.1rem;
    margin-bottom: 25px;
    opacity: 0.9;
}

.lunch-audio-player {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 15px;
}

.lunch-play-btn {
    width: 60px !important;
    height: 60px !important;
    min-width: 60px !important;
    background: rgba(255, 255, 255, 0.9) !important;
    color: #f57c00 !important;
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.2) !important;
}

.lunch-play-btn:hover {
    background: white !important;
    transform: scale(1.1);
}

.play-text {
    font-weight: 600;
    font-size: 1.1rem;
}

/* Categories Section */
.categories-section {
    margin: 80px 0;
}

.categories-title {
    font-size: 2rem;
    font-weight: 700;
    color: #1b5e20;
    text-align: center;
    margin-bottom: 40px;
}

.categories-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 25px;
}

.category-card {
    padding: 30px;
    text-align: center;
    border-radius: 16px;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
}

.category-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    opacity: 0;
    transition: opacity 0.3s ease;
}

.category-card:hover {
    transform: translateY(-5px);
}

.category-card:hover::before {
    opacity: 0.1;
}

.category-icon {
    font-size: 3rem;
    margin-bottom: 15px;
}

.category-name {
    font-size: 1.3rem;
    font-weight: 600;
    margin-bottom: 10px;
}

.category-description {
    margin-bottom: 15px;
    line-height: 1.5;
    opacity: 0.8;
}

.category-count {
    font-weight: 600;
    padding: 6px 12px;
    border-radius: 15px;
    background: rgba(0, 0, 0, 0.1);
    display: inline-block;
}

.category-informativo {
    background: linear-gradient(135deg, #e3f2fd, #bbdefb);
    color: #1565c0;
}

.category-cultural {
    background: linear-gradient(135deg, #f3e5f5, #e1bee7);
    color: #6a1b9a;
}

.category-educativo {
    background: linear-gradient(135deg, #e8f5e8, #c8e6c9);
    color: #2e7d32;
}

.category-deportivo {
    background: linear-gradient(135deg, #fff3e0, #ffe0b2);
    color: #ef6c00;
}

.category-entretenimiento {
    background: linear-gradient(135deg, #fce4ec, #f8bbd9);
    color: #c2185b;
}

.category-formativo {
    background: linear-gradient(135deg, #efebe9, #d7ccc8);
    color: #4e342e;
}

/* Special Programs Section */
.special-programs-section {
    margin: 80px 0;
}

.section-subtitle {
    font-size: 2rem;
    font-weight: 700;
    color: #1b5e20;
    text-align: center;
    margin-bottom: 40px;
}

.special-programs-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
    gap: 30px;
}

.special-program-card {
    border-radius: 20px;
    overflow: hidden;
    transition: all 0.3s ease;
}

.special-program-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
}

.special-program-header {
    padding: 30px;
    position: relative;
    color: white;
    text-align: center;
}

.special-icon {
    font-size: 3rem;
    margin-bottom: 15px;
}

.special-badge {
    position: absolute;
    top: 15px;
    right: 15px;
    background: rgba(255, 255, 255, 0.2);
    padding: 6px 12px;
    border-radius: 12px;
    font-size: 0.8rem;
    font-weight: 600;
    backdrop-filter: blur(10px);
}

.special-program-content {
    padding: 30px;
    background: white;
}

.special-title {
    font-size: 1.4rem;
    font-weight: 600;
    margin-bottom: 15px;
    color: #1b5e20;
}

.special-description {
    margin-bottom: 20px;
    line-height: 1.6;
    color: #666;
}

.special-details {
    display: flex;
    gap: 20px;
    flex-wrap: wrap;
}

.special-time,
.special-day {
    display: flex;
    align-items: center;
    gap: 8px;
    color: #2e7d32;
    font-weight: 500;
}

/* Participation Section */
.participation-section {
    margin: 80px 0 40px;
}

.participation-card {
    border-radius: 20px;
    background: linear-gradient(135deg, #2e7d32, #1b5e20) !important;
    position: relative;
    overflow: hidden;
}

.participation-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><path d="M0,100 Q50,50 100,100 L100,0 L0,0 Z" fill="rgba(255,255,255,0.05)"/></svg>');
    opacity: 0.3;
}

.participation-content {
    position: relative;
    z-index: 1;
    display: flex;
    align-items: center;
    gap: 40px;
    flex-wrap: wrap;
    padding: 20px;
}

.participation-text {
    flex: 1;
    min-width: 300px;
}

.participation-icon {
    margin-bottom: 20px;
    animation: pulse 2s ease-in-out infinite;
}

.participation-title {
    font-size: 2rem;
    font-weight: 700;
    margin-bottom: 15px;
}

.participation-description {
    font-size: 1.1rem;
    opacity: 0.9;
    line-height: 1.6;
}

.participation-actions {
    display: flex;
    gap: 15px;
    flex-wrap: wrap;
}

.participation-btn {
    font-weight: 600 !important;
    padding: 12px 24px !important;
    border-radius: 25px !important;
    transition: all 0.3s ease !important;
}

.participation-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
}

/* Responsive Design */
@media (max-width: 1200px) {
    .schedule-header,
    .time-row {
        grid-template-columns: 120px repeat(5, 1fr);
    }
    
    .time-cell {
        padding: 15px 10px;
    }
    
    .program-card {
        padding: 15px;
        min-height: 120px;
    }
    
    .program-title {
        font-size: 0.9rem;
    }
}

@media (max-width: 768px) {
    .hero-title {
        font-size: 2.5rem;
    }
    
    .schedule-header,
    .time-row {
        grid-template-columns: 100px repeat(5, 1fr);
    }
    
    .time-cell {
        padding: 10px 5px;
    }
    
    .time-text {
        font-size: 0.8rem;
        writing-mode: vertical-rl;
        text-orientation: mixed;
    }
    
    .program-cell {
        padding: 8px;
    }
    
    .program-card {
        padding: 12px;
        min-height: 100px;
    }
    
    .program-title {
        font-size: 0.8rem;
    }
    
    .program-description {
        font-size: 0.75rem;
    }
    
    .audio-player {
        position: static;
        margin-top: 10px;
        text-align: center;
    }
    
    .participation-content {
        flex-direction: column;
        text-align: center;
    }
    
    .participation-actions {
        justify-content: center;
    }
}

@media (max-width: 480px) {
    .hero-section {
        padding: 60px 0;
    }
    
    .hero-title {
        font-size: 2rem;
    }
    
    .schedule-section {
        padding: 60px 0;
    }
    
    .schedule-header,
    .time-row {
        display: block;
    }
    
    .time-row {
        margin-bottom: 20px;
        border: 1px solid #e0e0e0;
        border-radius: 12px;
        overflow: hidden;
    }
    
    .time-cell {
        text-align: center;
        background: #2e7d32;
        color: white;
        padding: 15px;
    }
    
    .time-text {
        writing-mode: initial;
        font-size: 1rem;
        font-weight: 600;
    }
    
    .program-cell {
        padding: 15px;
        border-right: none;
        border-bottom: 1px solid #e0e0e0;
    }
    
    .program-cell:last-child {
        border-bottom: none;
    }
    
    .program-card {
        min-height: auto;
    }
    
    .categories-grid {
        grid-template-columns: 1fr;
    }
    
    .special-programs-grid {
        grid-template-columns: 1fr;
    }
}

.program-musical {
    background: linear-gradient(135deg, #ff9800, #f57c00);
    color: white;
}

.category-musical {
    background: linear-gradient(135deg, #fff3e0, #ffe0b2);
    color: #ef6c00;
}
</style>