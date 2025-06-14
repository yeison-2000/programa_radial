<template>
    <footer class="modern-footer">
        <!-- Wave Effect Superior -->
        <div class="top-wave">
            <svg viewBox="0 0 1200 120" preserveAspectRatio="none">
                <path d="M0,0V60c0,0,200,30,600,0s600,30,600,0V0z" class="wave-path"></path>
            </svg>
        </div>

        <!-- Contenido Principal del Footer -->
        <div class="footer-content">
            <v-container>
                <div class="footer-grid">

                    <!-- Sección Institucional -->
                    <div class="footer-section institutional-section">
                        <div class="logo-footer mb-4">
                            <img class="image" src="/public/img/image.png" alt="">
                            <h3 class="footer-title">Emisora Escolar</h3>
                            <p class="footer-subtitle">Santa María Goretti</p>
                        </div>

                        <p class="institutional-description">
                            Formando líderes con valores, para un futuro mejor.
                            En Santa María Goretti inspiramos la valentía el perdón y la paz en cada estudiante.
                            Nuestra emisora escolar es un espacio para aprender, compartir y crecer juntos.
                        </p>

                        <!-- Redes Sociales -->
                        <div class="social-links">
                            <v-btn v-for="social in socialLinks" :key="social.name" :icon="social.icon"
                                :href="social.url" target="_blank" variant="text" class="social-btn"
                                size="large"></v-btn>
                        </div>
                    </div>

                    <!-- Enlaces Rápidos -->
                    <div class="footer-section quick-links-section">
                        <h4 class="section-title">
                            <v-icon class="title-icon">mdi-link</v-icon>
                            Enlaces Rápidos
                        </h4>
                        <ul class="quick-links-list">
                            <li v-for="link in quickLinks" :key="link.name" class="quick-link-item">
                                <router-link :to="link.route" class="quick-link">
                                    <v-icon class="link-icon" size="small">{{ link.icon }}</v-icon>
                                    {{ link.name }}
                                </router-link>
                            </li>
                        </ul>
                    </div>

                    <!-- Información de Contacto -->
                    <div class="footer-section contact-section">
                        <h4 class="section-title">
                            <v-icon class="title-icon">mdi-phone</v-icon>
                            Contacto
                        </h4>
                        <div class="contact-info">
                            <div class="contact-item">
                                <v-icon class="contact-icon">mdi-map-marker</v-icon>
                                <div class="contact-text">
                                    <span class="contact-label">Dirección:</span>
                                    <span class="contact-value">Montería, Córdoba</span>
                                </div>
                            </div>

                            <div class="contact-item">
                                <v-icon class="contact-icon">mdi-email</v-icon>
                                <div class="contact-text">
                                    <span class="contact-label">Email:</span>
                                    <span class="contact-value">emisora@smg.edu.co</span>
                                </div>
                            </div>

                            <div class="contact-item">
                                <v-icon class="contact-icon">mdi-clock</v-icon>
                                <div class="contact-text">
                                    <span class="contact-label">Horario:</span>
                                    <span class="contact-value">Lun - Vie: 8:00 AM - 3:00 PM</span>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Programación Destacada -->
                    <div class="footer-section programs-section">
                        <h4 class="section-title">
                            <v-icon class="title-icon">mdi-radio</v-icon>
                            En Vivo Ahora
                        </h4>

                        <div class="live-program">
                            <div class="live-indicator">
                                <div class="pulse-dot"></div>
                                <span class="live-text">EN VIVO</span>
                            </div>

                            <div class="program-info">
                                <h5 class="program-name">{{ currentProgram.name }}</h5>
                                <p class="program-time">{{ currentProgram.time }}</p>
                                <p class="program-description">{{ currentProgram.description }}</p>
                            </div>
                        </div>

                        <!-- Próximo Programa -->
                        <div class="next-program">
                            <span class="next-label">Próximo:</span>
                            <span class="next-program-name">{{ nextProgram.name }}</span>
                            <span class="next-program-time">{{ nextProgram.time }}</span>
                        </div>
                    </div>

                </div>
            </v-container>
        </div>

        <!-- Footer Bottom -->
        <div class="footer-bottom">
            <v-container>
                <div class="bottom-content">
                    <div class="copyright-section">
                        <p class="copyright-text">
                            © {{ currentYear }} Emisora Escolar - Institución Educativa Santa María Goretti. Todos los derechos reservados.
                        </p>
                        <p class="slogan">
                            🌹 "Formando líderes con valores, construyendo el futuro con esperanza" 🌹
                        </p>
                    </div>

                    <div class="footer-actions">
                        <v-btn variant="outlined" size="small" class="action-btn" prepend-icon="mdi-heart">
                            Apóyanos
                        </v-btn>

                        <v-btn variant="text" size="small" class="action-btn" prepend-icon="mdi-arrow-up"
                            @click="scrollToTop">
                            Subir
                        </v-btn>
                    </div>
                </div>
            </v-container>
        </div>

        <!-- Floating Elements -->
        <div class="floating-elements">
            <div class="floating-element element-1">🎵</div>
            <div class="floating-element element-2">📻</div>
            <div class="floating-element element-3">🎤</div>
            <div class="floating-element element-4">🌟</div>
        </div>
    </footer>
</template>

<script>
export default {
    name: 'ModernFooter',

    data() {
        return {
            currentYear: new Date().getFullYear(),

            socialLinks: [
                {
                    name: 'Facebook',
                    icon: 'mdi-facebook',
                    url: 'https://www.facebook.com/iesamagoretti?locale=es_LA'
                },
                {
                    name: 'Instagram',
                    icon: 'mdi-instagram',
                    url: 'https://www.instagram.com/somosgoretti/'
                },
                {
                    name: 'YouTube',
                    icon: 'mdi-youtube',
                    url: 'https://www.youtube.com/watch?v=cWMR1fAgYRQ&ab_channel=TV5ElCanaldeMonter%C3%ADa'
                },
                {
                    name: 'WhatsApp',
                    icon: 'mdi-whatsapp',
                    url: 'https://w.app/0ltzqv'
                }
            ],

            quickLinks: [
                { name: 'Inicio', route: '/', icon: 'mdi-home' },
                { name: 'Documentación', route: '/documentacion', icon: 'mdi-book-open-variant' },
                { name: 'Galería', route: '/galeria', icon: 'mdi-image-multiple' },
                { name: 'Programación', route: '/programacion', icon: 'mdi-calendar-clock' },
                { name: 'Programas', route: '/programas', icon: 'mdi-radio' },
                { name: 'Nuestro Equipo', route: '/creditos', icon: 'mdi-account-group' }
            ],

            currentProgram: {
                name: 'Noticias Goretianas',
                time: '8:00 - 9:00 AM',
                description: 'Las noticias más importantes de nuestra institución'
            },

            nextProgram: {
                name: 'Historia y Tradición',
                time: '9:00 - 10:00 AM'
            }
        }
    },

    methods: {
        scrollToTop() {
            window.scrollTo({
                top: 0,
                behavior: 'smooth'
            })
        }
    }
}
</script>

<style scoped>
/* Footer Principal */
.modern-footer {
    background: linear-gradient(180deg, #1b5e20 0%, #2e7d32 50%, #1b5e20 100%);
    position: relative;
    margin-top: auto;
    overflow: hidden;
}

/* Wave Effect Superior */
.top-wave {
    position: absolute;
    top: -1px;
    left: 0;
    width: 100%;
    height: 60px;
    z-index: 1;
    
}

.wave-path {
    fill: green;
    animation: waveMove 6s ease-in-out infinite;
}

@keyframes waveMove {

    0%,
    100% {
        d: path("M0,0V60c0,0,200,30,600,0s600,30,600,0V0z");
    }

    50% {
        d: path("M0,0V60c0,0,200,0,600,30s600,0,600,30V0z");
    }
}

/* Contenido del Footer */
.footer-content {
    position: relative;
    z-index: 2;
    padding: 80px 0 40px;
}

.footer-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 40px;
    align-items: start;
}

/* Secciones del Footer */
.footer-section {
    background: rgba(205, 26, 26, 0.05);
    padding: 30px;
    border-radius: 20px;
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.1);
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
    overflow: hidden;
}

.footer-section::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.05), transparent);
    transition: left 0.8s;
}

.footer-section:hover::before {
    left: 100%;
}

.footer-section:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(216, 6, 6, 0.3);
    border-color: rgba(129, 199, 132, 0.3);
}

/* Logo del Footer */
.footer-logo-avatar {
    background: linear-gradient(135deg, #fff 0%, #f1f8e9 100%) !important;
    box-shadow: 0 8px 25px rgba(220, 52, 52, 0.815);
    border: 3px solid rgba(233, 88, 88, 0.868);
}

.footer-logo-emoji {
    font-size: 32px;
    animation: floatRotate 4s ease-in-out infinite;
}

@keyframes floatRotate {

    0%,
    100% {
        transform: rotate(0deg) translateY(0px);
    }

    25% {
        transform: rotate(5deg) translateY(-5px);
    }

    75% {
        transform: rotate(-5deg) translateY(5px);
    }
}

.footer-title {
    color: white;
    font-weight: 700;
    font-size: 1.5rem;
    margin-bottom: 5px;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    background: linear-gradient(45deg, #fff, #a5d6a7);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

.footer-subtitle {
    color: rgba(255, 255, 255, 0.8);
    font-size: 1rem;
    margin: 0;
    font-weight: 500;
}

/* Descripción Institucional */
.institutional-description {
    color: rgba(255, 255, 255, 0.9);
    line-height: 1.6;
    margin: 20px 0;
    font-size: 0.95rem;
}

/* Redes Sociales */
.social-links {
    display: flex;
    gap: 10px;
    margin-top: 20px;
}

.social-btn {
    background: rgba(255, 255, 255, 0.1) !important;
    color: white !important;
    border-radius: 50%;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.social-btn:hover {
    background: rgba(129, 199, 132, 0.3) !important;
    transform: scale(1.1) rotate(5deg);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

/* Títulos de Sección */
.section-title {
    color: #a5d6a7;
    font-weight: 600;
    font-size: 1.2rem;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 10px;
}

.title-icon {
    color: #81c784;
    font-size: 1.3rem;
}

/* Enlaces Rápidos */
.quick-links-list {
    list-style: none;
    padding: 0;
    margin: 0;
}

.quick-link-item {
    margin-bottom: 12px;
}

.quick-link {
    color: rgba(255, 255, 255, 0.8);
    text-decoration: none;
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 8px 0;
    transition: all 0.3s ease;
    font-size: 0.95rem;
}

.quick-link:hover {
    color: #a5d6a7;
    transform: translateX(10px);
}

.link-icon {
    color: #81c784;
    transition: all 0.3s ease;
}

.quick-link:hover .link-icon {
    color: #c8e6c9;
    transform: scale(1.2);
}

/* Información de Contacto */
.contact-info {
    display: flex;
    flex-direction: column;
    gap: 15px;
}

.contact-item {
    display: flex;
    align-items: flex-start;
    gap: 12px;
}

.contact-icon {
    color: #81c784;
    font-size: 1.2rem;
    margin-top: 2px;
}

.contact-text {
    display: flex;
    flex-direction: column;
    gap: 2px;
}

.contact-label {
    color: rgba(255, 255, 255, 0.7);
    font-size: 0.85rem;
    font-weight: 500;
}

.contact-value {
    color: white;
    font-size: 0.95rem;
}

/* Programa en Vivo */
.live-program {
    background: rgba(255, 255, 255, 0.05);
    padding: 20px;
    border-radius: 15px;
    border: 1px solid rgba(129, 199, 132, 0.3);
    margin-bottom: 15px;
}

.live-indicator {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-bottom: 10px;
}

.pulse-dot {
    width: 12px;
    height: 12px;
    background: #f44336;
    border-radius: 50%;
    animation: pulse 1.5s ease-in-out infinite;
}

@keyframes pulse {

    0%,
    100% {
        opacity: 1;
        transform: scale(1);
    }

    50% {
        opacity: 0.5;
        transform: scale(1.2);
    }
}

.live-text {
    color: #f44336;
    font-weight: 700;
    font-size: 0.8rem;
    letter-spacing: 1px;
}

.program-name {
    color: white;
    font-weight: 600;
    margin-bottom: 5px;
}

.program-time {
    color: #a5d6a7;
    font-size: 0.9rem;
    margin-bottom: 8px;
}

.program-description {
    color: rgba(255, 255, 255, 0.8);
    font-size: 0.85rem;
    line-height: 1.4;
    margin: 0;
}

/* Próximo Programa */
.next-program {
    display: flex;
    align-items: center;
    gap: 8px;
    flex-wrap: wrap;
}

.next-label {
    color: rgba(255, 255, 255, 0.7);
    font-size: 0.85rem;
}

.next-program-name {
    color: white;
    font-weight: 500;
    font-size: 0.9rem;
}

.next-program-time {
    color: #81c784;
    font-size: 0.85rem;
}

/* Footer Bottom */
.footer-bottom {
    background: rgba(0, 0, 0, 0.2);
    padding: 25px 0;
    border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.bottom-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 20px;
}

.copyright-text {
    color: rgba(255, 255, 255, 0.8);
    font-size: 0.9rem;
    margin: 0;
}

.slogan {
    color: rgba(255, 255, 255, 0.9);
    font-size: 0.95rem;
    font-style: italic;
    margin: 5px 0 0 0;
}

.footer-actions {
    display: flex;
    gap: 15px;
}

.action-btn {
    color: white !important;
    border-color: rgba(255, 255, 255, 0.3) !important;
    transition: all 0.3s ease;
}

.action-btn:hover {
    background: rgba(255, 255, 255, 0.1) !important;
    border-color: #81c784 !important;
    transform: translateY(-2px);
}

/* Elementos Flotantes */
.floating-elements {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    pointer-events: none;
    z-index: 1;
}

.floating-element {
    position: absolute;
    font-size: 2rem;
    opacity: 0.1;
    animation: float 8s ease-in-out infinite;
}

.element-1 {
    top: 20%;
    left: 10%;
    animation-delay: 0s;
}

.element-2 {
    top: 60%;
    right: 15%;
    animation-delay: 2s;
}

.element-3 {
    bottom: 30%;
    left: 20%;
    animation-delay: 4s;
}

.element-4 {
    top: 40%;
    right: 30%;
    animation-delay: 6s;
}

@keyframes float {

    0%,
    100% {
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

/* Responsive */
@media (max-width: 960px) {
    .footer-grid {
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 30px;
    }

    .footer-content {
        padding: 60px 0 30px;
    }

    .bottom-content {
        flex-direction: column;
        text-align: center;
    }
}

@media (max-width: 600px) {
    .footer-section {
        padding: 20px;
    }

    .footer-grid {
        grid-template-columns: 1fr;
        gap: 20px;
    }

    .social-links {
        justify-content: center;
    }

    .next-program {
        flex-direction: column;
        align-items: flex-start;
        gap: 5px;
    }
}

/* Animación de entrada */
.modern-footer {
    animation: slideUp 1s cubic-bezier(0.4, 0, 0.2, 1);
}

@keyframes slideUp {
    from {
        transform: translateY(100px);
        opacity: 0;
    }

    to {
        transform: translateY(0);
        opacity: 1;
    }
}
.image {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    margin-right: 16px;
}
</style>