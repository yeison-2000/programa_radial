<template>
    <div class="documentacion-page">
        <!-- Hero Section -->
        <section class="hero-section">
            <div class="hero-background">
                <div class="floating-icons">
                    <div class="icon icon-1">📚</div>
                    <div class="icon icon-2">🏫</div>
                    <div class="icon icon-3">📋</div>
                    <div class="icon icon-4">🌟</div>
                    <div class="icon icon-5">📖</div>
                </div>
            </div>

            <v-container>
                <div class="hero-content">
                    <div class="hero-badge">
                        <v-icon class="doc-icon">mdi-book-open-page-variant</v-icon>
                        <span>DOCUMENTACIÓN</span>
                    </div>

                    <h1 class="hero-title">
                        Información
                        <span class="title-highlight">Institucional</span>
                    </h1>

                    <p class="hero-description">
                        Encuentra toda la información relevante sobre nuestra institución, 
                        conecta con nosotros en redes sociales y accede a nuestros canales 
                        de comunicación oficial.
                    </p>
                </div>
            </v-container>
        </section>

        <!-- Main Content -->
        <section class="content-section">
            <v-container>
                <div class="content-grid">
                    <!-- Información General -->
                    <v-card class="info-card" elevation="8">
                        <div class="card-header info-header">
                            <v-icon size="x-large" color="white">mdi-information</v-icon>
                            <h3>Información General</h3>
                        </div>
                        <v-card-text class="card-content">
                            <div class="info-item">
                                <v-icon color="green-darken-2" class="info-icon">mdi-school</v-icon>
                                <div>
                                    <h4>Nombre Completo</h4>
                                    <p>Institución Educativa Santa María Goretti</p>
                                </div>
                            </div>
                            <div class="info-item">
                                <v-icon color="green-darken-3" class="info-icon">mdi-map-marker</v-icon>
                                <div>
                                    <h4>Ubicación</h4>
                                    <p>Montería, Córdoba, Colombia</p>
                                </div>
                            </div>
                            <div class="info-item">
                                <v-icon color="green-darken-1" class="info-icon">mdi-account-group</v-icon>
                                <div>
                                    <h4>Modalidad</h4>
                                    <p>Educación Básica y Media</p>
                                </div>
                            </div>
                            <div class="info-item">
                                <v-icon color="green-accent-4" class="info-icon">mdi-radio</v-icon>
                                <div>
                                    <h4>Proyecto Especial</h4>
                                    <p>Emisora Escolar SMG Radio</p>
                                </div>
                            </div>
                        </v-card-text>
                    </v-card>

                    <!-- Redes Sociales -->
                    <v-card class="social-card" elevation="8">
                        <div class="card-header social-header">
                            <v-icon size="x-large" color="white">mdi-share-variant</v-icon>
                            <h3>Redes Sociales</h3>
                        </div>
                        <v-card-text class="card-content">
                            <p class="social-intro">Síguenos y mantente conectado con todas nuestras actividades</p>
                            
                            <div class="social-buttons">
                                <v-btn
                                    v-for="social in socialNetworks"
                                    :key="social.name"
                                    :color="social.color"
                                    :href="social.url"
                                    target="_blank"
                                    size="large"
                                    variant="elevated"
                                    class="social-btn"
                                    @click="trackSocialClick(social.name)"
                                >
                                    <v-icon start>{{ social.icon }}</v-icon>
                                    {{ social.name }}
                                </v-btn>
                            </div>

                            <div class="social-stats">
                                <div class="stat-card" v-for="stat in socialStats" :key="stat.platform">
                                    <v-icon :color="stat.color" size="large">{{ stat.icon }}</v-icon>
                                    <div class="stat-info">
                                        <div class="stat-number">{{ stat.followers }}</div>
                                        <div class="stat-label">{{ stat.platform }}</div>
                                    </div>
                                </div>
                            </div>
                        </v-card-text>
                    </v-card>

                    <!-- Contacto -->
                    <v-card class="contact-card" elevation="8">
                        <div class="card-header contact-header">
                            <v-icon size="x-large" color="white">mdi-phone</v-icon>
                            <h3>Contacto</h3>
                        </div>
                        <v-card-text class="card-content">
                            <div class="contact-methods">
                                <div class="contact-item">
                                    <v-btn
                                        color="green-darken-2"
                                        variant="outlined"
                                        size="large"
                                        class="contact-btn"
                                        @click="openContact('email')"
                                    >
                                        <v-icon start>mdi-email</v-icon>
                                        Correo Electrónico
                                    </v-btn>
                                </div>
                                <div class="contact-item">
                                    <v-btn
                                        color="green-darken-1"
                                        variant="outlined"
                                        size="large"
                                        class="contact-btn"
                                        @click="openContact('phone')"
                                    >
                                        <v-icon start>mdi-phone</v-icon>
                                        Teléfono
                                    </v-btn>
                                </div>
                                <div class="contact-item">
                                    <v-btn
                                        color="green-accent-4"
                                        variant="outlined"
                                        size="large"
                                        class="contact-btn"
                                        @click="openContact('location')"
                                    >
                                        <v-icon start>mdi-map</v-icon>
                                        Ver Ubicación
                                    </v-btn>
                                </div>
                            </div>
                        </v-card-text>
                    </v-card>

                    <!-- Recursos -->
                    <v-card class="resources-card" elevation="8">
                        <div class="card-header resources-header">
                            <v-icon size="x-large" color="white">mdi-folder-multiple</v-icon>
                            <h3>Recursos</h3>
                        </div>
                        <v-card-text class="card-content">
                            <div class="resources-grid">
                                <div class="resource-item" v-for="resource in resources" :key="resource.name">
                                    <v-card 
                                        class="resource-card-inner" 
                                        elevation="2"
                                        @click="accessResource(resource)"
                                        :disabled="!resource.available"
                                    >
                                        <v-card-text class="resource-content">
                                            <v-icon 
                                                :color="resource.available ? resource.color : 'grey'" 
                                                size="large"
                                                class="resource-icon"
                                            >
                                                {{ resource.icon }}
                                            </v-icon>
                                            <h4 class="resource-title">{{ resource.name }}</h4>
                                            <p class="resource-description">{{ resource.description }}</p>
                                            <v-chip 
                                                :color="resource.available ? 'green' : 'grey'"
                                                size="small"
                                                variant="outlined"
                                            >
                                                {{ resource.available ? 'Disponible' : 'Próximamente' }}
                                            </v-chip>
                                        </v-card-text>
                                    </v-card>
                                </div>
                            </div>
                        </v-card-text>
                    </v-card>
                </div>
            </v-container>
        </section>

        <!-- Quick Actions -->
        <section class="actions-section">
            <v-container>
                <div class="actions-content">
                    <h2 class="actions-title">Acciones Rápidas</h2>
                    <div class="quick-actions">
                        <v-btn
                            color="green-darken-2"
                            size="large"
                            variant="elevated"
                            class="action-btn"
                            @click="scrollToTop"
                        >
                            <v-icon start>mdi-arrow-up</v-icon>
                            Volver Arriba
                        </v-btn>
                        <v-btn
                            color="green-darken-1"
                            size="large"
                            variant="elevated"
                            class="action-btn"
                            @click="shareInstitution"
                        >
                            <v-icon start>mdi-share</v-icon>
                            Compartir
                        </v-btn>
                        <v-btn
                            color="green-accent-4"
                            size="large"
                            variant="elevated"
                            class="action-btn"
                            @click="downloadInfo"
                        >
                            <v-icon start>mdi-download</v-icon>
                            Descargar Info
                        </v-btn>
                    </div>
                </div>
            </v-container>
        </section>

        <!-- Snackbar for notifications -->
        <v-snackbar
            v-model="snackbar.show"
            :color="snackbar.color"
            :timeout="3000"
            location="bottom"
        >
            {{ snackbar.message }}
            <template v-slot:actions>
                <v-btn variant="text" @click="snackbar.show = false">
                    Cerrar
                </v-btn>
            </template>
        </v-snackbar>
    </div>
</template>

<script>
export default {
    name: "DocumentacionPage",

    data() {
        return {
            snackbar: {
                show: false,
                message: '',
                color: 'success'
            },

            socialNetworks: [
                {
                    name: 'Facebook',
                    icon: 'mdi-facebook',
                    color: 'green-darken-2',
                    url: 'https://www.facebook.com/iesamagoretti?locale=es_LA'
                },
                {
                    name: 'Instagram',
                    icon: 'mdi-instagram',
                    color: 'green-darken-1',
                    url: 'https://www.instagram.com/somosgoretti?utm_source=ig_web_button_share_sheet&igsh=ZDNlZDc0MzIxNw=='
                },
                {
                    name: 'Twitter',
                    icon: 'mdi-twitter',
                    color: 'green-accent-3',
                    url: 'https://x.com/sofym0729?t=P9kDj1GbZeE9CYGpCKXrdw&s=09'
                },
                {
                    name: 'YouTube',
                    icon: 'mdi-youtube',
                    color: 'green-accent-4',
                    url: 'https://youtu.be/cWMR1fAgYRQ?feature=shared'
                }
            ],

            socialStats: [
                {
                    platform: 'Facebook',
                    followers: '4960',
                    icon: 'mdi-facebook',
                    color: 'green-darken-2'
                },
                {
                    platform: 'Instagram',
                    followers: '533',
                    icon: 'mdi-instagram',
                    color: 'green-darken-1'
                },
                {
                    platform: 'YouTube',
                    followers: '4.74K',
                    icon: 'mdi-youtube',
                    color: 'green-accent-4'
                }
            ],

            resources: [
                {
                    name: 'Manual Estudiantil',
                    description: 'Normas y reglamentos institucionales',
                    icon: 'mdi-book-open',
                    color: 'green-darken-2',
                    available: false
                },
                {
                    name: 'Calendario Académico',
                    description: 'Fechas importantes del año escolar',
                    icon: 'mdi-calendar',
                    color: 'green-darken-1',
                    available: true
                },
                {
                    name: 'Programas Radiales',
                    description: 'Acceso a nuestros contenidos de radio',
                    icon: 'mdi-radio',
                    color: 'green-accent-3',
                    available: true
                },
                {
                    name: 'Galería Fotográfica',
                    description: 'Momentos destacados de la institución',
                    icon: 'mdi-camera',
                    color: 'green-accent-4',
                    available: true
                }
            ]
        };
    },

    methods: {
        trackSocialClick(platform) {
            this.showSnackbar(`Redirigiendo a ${platform}...`, 'info');
        },

        openContact(type) {
            const contacts = {
                email: 'ymorelochavez49@correo.unicordoba.edu.co',
                phone: '+57 3218669145',
                location: 'https://www.google.com/maps/place/Instituci%C3%B3n+Educativa+Santa+Mar%C3%ADa+Goretti/@8.7348054,-75.8877499,17z/data=!3m1!4b1!4m6!3m5!1s0x8e5a301a7eca3bad:0xa84052eab7748038!8m2!3d8.7348054!4d-75.885175!16s%2Fg%2F11c529qbvk?entry=ttu&g_ep=EgoyMDI1MDYxMS4wIKXMDSoASAFQAw%3D%3D'
            };

            switch(type) {
                case 'email':
                    window.open(`mailto:${contacts.email}`);
                    this.showSnackbar('Abriendo cliente de correo...', 'success');
                    break;
                case 'phone':
                    this.showSnackbar(`Teléfono: ${contacts.phone}`, 'info');
                    break;
                case 'location':
                    window.open(contacts.location, '_blank');
                    this.showSnackbar('Abriendo mapa...', 'success');
                    break;
            }
        },

        accessResource(resource) {
            if (resource.available) {
                if (resource.name === 'Programas Radiales') {
                    this.$router.push('/programas');
                    this.showSnackbar('Redirigiendo a programas...', 'success');
                } else {
                    this.showSnackbar(`Accediendo a ${resource.name}...`, 'success');
                }
            } else {
                this.showSnackbar('Este recurso estará disponible próximamente', 'warning');
            }
            if (resource.available) {
                if (resource.name === 'Galería Fotográfica') {
                    this.$router.push('/galeria');
                } else {
                    this.showSnackbar(`Accediendo a ${resource.name}...`, 'success');
                }
            } else {
                this.showSnackbar('Este recurso estará disponible próximamente', 'warning');
            }
            if (resource.available) {
                if (resource.name === 'Calendario Académico') {
                    this.$router.push('/programacion');
                } else {
                    this.showSnackbar(`Accediendo a ${resource.name}...`, 'success');
                }
            } else {
                this.showSnackbar('Este recurso estará disponible próximamente', 'warning');
            }
        },

        scrollToTop() {
            window.scrollTo({ top: 0, behavior: 'smooth' });
            this.showSnackbar('Volviendo al inicio...', 'info');
        },

        shareInstitution() {
            if (navigator.share) {
                navigator.share({
                    title: 'I.E. Santa María Goretti',
                    text: 'Conoce nuestra institución educativa en Montería, Córdoba',
                    url: `https://www.google.com/maps/place/Instituci%C3%B3n+Educativa+Santa+Mar%C3%ADa+Goretti/@8.7348054,-75.8877499,17z/data=!3m1!4b1!4m6!3m5!1s0x8e5a301a7eca3bad:0xa84052eab7748038!8m2!3d8.7348054!4d-75.885175!16s%2Fg%2F11c529qbvk?entry=ttu&g_ep=EgoyMDI1MDYxMS4wIKXMDSoASAFQAw%3D%3D`
                });
            } else {
                navigator.clipboard.writeText(window.location.href);
                this.showSnackbar('Enlace copiado al portapapeles', 'success');
            }
        },

        downloadInfo() {
            // Simular descarga de información institucional
            this.showSnackbar('La descarga comenzará próximamente...', 'warning');
        },

        showSnackbar(message, color = 'success') {
            this.snackbar.message = message;
            this.snackbar.color = color;
            this.snackbar.show = true;
        }
    }
};
</script>

<style scoped>
.documentacion-page {
    min-height: 100vh;
    background: linear-gradient(135deg, #f1f8e9 0%, #c8e6c9 100%);
}

/* Hero Section */
.hero-section {
    position: relative;
    padding: 80px 0;
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

.floating-icons {
    position: absolute;
    width: 100%;
    height: 100%;
    pointer-events: none;
}

.icon {
    position: absolute;
    font-size: 2rem;
    opacity: 0.1;
    animation: float-icon 8s ease-in-out infinite;
}

.icon-1 { top: 20%; left: 10%; animation-delay: 0s; }
.icon-2 { top: 30%; right: 15%; animation-delay: 2s; }
.icon-3 { bottom: 30%; left: 20%; animation-delay: 4s; }
.icon-4 { bottom: 20%; right: 10%; animation-delay: 6s; }
.icon-5 { top: 50%; left: 80%; animation-delay: 1s; }

@keyframes float-icon {
    0%, 100% {
        transform: translateY(0px) rotate(0deg);
        opacity: 0.1;
    }
    50% {
        transform: translateY(-20px) rotate(180deg);
        opacity: 0.3;
    }
}

.hero-content {
    position: relative;
    z-index: 2;
    text-align: center;
    max-width: 700px;
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

.doc-icon {
    animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.1); }
}

.hero-title {
    font-size: 3rem;
    font-weight: 700;
    margin-bottom: 20px;
    line-height: 1.2;
}

.title-highlight {
    background: linear-gradient(45deg, #81c784, #a5d6a7);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

.hero-description {
    font-size: 1.1rem;
    margin-bottom: 30px;
    opacity: 0.9;
    line-height: 1.6;
}

/* Content Section */
.content-section {
    padding: 60px 0;
}

.content-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
    gap: 30px;
}

.info-card, .social-card, .contact-card, .resources-card {
    border-radius: 15px;
    overflow: hidden;
    transition: all 0.3s ease;
}

.info-card:hover, .social-card:hover, .contact-card:hover, .resources-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.15);
}

.card-header {
    padding: 25px;
    color: white;
    display: flex;
    align-items: center;
    gap: 15px;
}

.info-header {
    background: linear-gradient(135deg, #2e7d32, #388e3c);
}

.social-header {
    background: linear-gradient(135deg, #1b5e20, #2e7d32);
}

.contact-header {
    background: linear-gradient(135deg, #388e3c, #43a047);
}

.resources-header {
    background: linear-gradient(135deg, #4caf50, #66bb6a);
}

.card-header h3 {
    font-size: 1.3rem;
    font-weight: 600;
    margin: 0;
}

.card-content {
    padding: 25px;
}

/* Info Card */
.info-item {
    display: flex;
    align-items: flex-start;
    gap: 15px;
    margin-bottom: 20px;
}

.info-icon {
    margin-top: 2px;
}

.info-item h4 {
    font-size: 1rem;
    font-weight: 600;
    color: #2e7d32;
    margin-bottom: 5px;
}

.info-item p {
    color: #666;
    margin: 0;
}

/* Social Card */
.social-intro {
    text-align: center;
    margin-bottom: 25px;
    color: #666;
}

.social-buttons {
    display: flex;
    flex-direction: column;
    gap: 12px;
    margin-bottom: 30px;
}

.social-btn {
    justify-content: flex-start;
    text-transform: none;
    font-weight: 600;
}

.social-stats {
    display: flex;
    justify-content: space-around;
    gap: 15px;
}

.stat-card {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 15px;
    background: #f1f8e9;
    border-radius: 10px;
    flex: 1;
    min-width: 0;
}

.stat-info {
    text-align: center;
    flex: 1;
}

.stat-number {
    font-size: 1.2rem;
    font-weight: 700;
    color: #2e7d32;
}

.stat-label {
    font-size: 0.8rem;
    color: #666;
}

/* Contact Card */
.contact-methods {
    display: flex;
    flex-direction: column;
    gap: 15px;
}

.contact-btn {
    width: 100%;
    justify-content: flex-start;
    text-transform: none;
    font-weight: 600;
}

/* Resources Card */
.resources-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 15px;
}

.resource-card-inner {
    border-radius: 10px;
    transition: all 0.3s ease;
    cursor: pointer;
    border: 1px solid #e8f5e8;
}

.resource-card-inner:not(.v-card--disabled):hover {
    transform: translateY(-3px);
    box-shadow: 0 8px 20px rgba(46, 125, 50, 0.15);
    border-color: #81c784;
}

.resource-content {
    text-align: center;
    padding: 20px 15px;
}

.resource-icon {
    margin-bottom: 10px;
}

.resource-title {
    font-size: 1rem;
    font-weight: 600;
    margin-bottom: 8px;
    color: #2e7d32;
}

.resource-description {
    font-size: 0.85rem;
    color: #666;
    margin-bottom: 15px;
    line-height: 1.4;
}

/* Actions Section */
.actions-section {
    padding: 40px 0;
    background: #f1f8e9;
}

.actions-content {
    text-align: center;
}

.actions-title {
    font-size: 2rem;
    font-weight: 600;
    color: #2e7d32;
    margin-bottom: 30px;
}

.quick-actions {
    display: flex;
    justify-content: center;
    gap: 20px;
    flex-wrap: wrap;
}

.action-btn {
    font-weight: 600;
    text-transform: none;
    border-radius: 25px;
    padding: 0 25px;
}

/* Responsive Design */
@media (max-width: 768px) {
    .hero-title {
        font-size: 2.2rem;
    }
    
    .content-grid {
        grid-template-columns: 1fr;
        gap: 20px;
    }
    
    .social-stats {
        flex-direction: column;
    }
    
    .quick-actions {
        flex-direction: column;
        align-items: center;
    }
    
    .action-btn {
        width: 250px;
    }
    
    .resources-grid {
        grid-template-columns: 1fr;
    }
}

@media (max-width: 480px) {
    .hero-section {
        padding: 50px 0;
    }
    
    .hero-title {
        font-size: 1.8rem;
    }
    
    .content-section {
        padding: 40px 0;
    }
    
    .card-header {
        padding: 20px;
    }
    
    .card-content {
        padding: 20px;
    }
    
    .actions-section {
        padding: 30px 0;
    }
    
    .actions-title {
        font-size: 1.5rem;
    }
}
</style>