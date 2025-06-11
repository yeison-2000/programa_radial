<template>
    <div>
        <!-- App Bar Principal -->
        <v-app-bar :elevation="scrolled ? 8 : 2" :class="{ 'scrolled': scrolled }" class="header-bar" fixed app
            height="80">
            <!-- Gradient Overlay -->
            <div class="gradient-overlay"></div>

            <v-container class="d-flex align-center pa-0" fluid>
                <!-- Logo y Título -->
                <div class="logo-section d-flex align-center">
                    <img class="image" src="/public/img/image.png" alt="">

                    <div class="title-section">
                        <h1 class="main-title">
                            Emisora Escolar
                        </h1>
                        <p class="institution-subtitle">
                            Institución Educativa Santa María Goretti
                        </p>
                    </div>
                </div>

                <v-spacer></v-spacer>

                <!-- Navegación Desktop -->
                <nav class="desktop-nav d-none d-lg-flex">
                    <v-btn v-for="item in navigationItems" :key="item.name" :to="item.route" variant="text"
                        class="nav-btn mx-1" :prepend-icon="item.icon" size="large">
                        {{ item.name }}
                    </v-btn>
                </nav>

                <!-- Botón Menú Mobile -->
                <v-btn icon class="d-lg-none" @click="drawer = !drawer" size="large">
                    <v-icon>mdi-menu</v-icon>
                </v-btn>
            </v-container>

            <!-- Wave Effect -->
            <div class="wave-effect"></div>
        </v-app-bar>

        <!-- Navigation Drawer para Mobile -->
        <v-navigation-drawer v-model="drawer" temporary location="right" class="mobile-drawer" width="320">
            <!-- Header del Drawer -->
            <div class="drawer-header">
                <img class="image" src="/public/img/image.png" alt="">
                <h3 class="drawer-title">Emisora Escolar</h3>
                <p class="drawer-subtitle">Santa Rosa de Lima</p>
            </div>

            <v-divider></v-divider>

            <!-- Lista de Navegación -->
            <v-list class="mobile-nav-list">
                <v-list-item v-for="item in navigationItems" :key="item.name" :to="item.route" class="mobile-nav-item"
                    @click="drawer = false">
                    <template v-slot:prepend>
                        <v-icon class="nav-icon">{{ item.icon }}</v-icon>
                    </template>

                    <v-list-item-title class="nav-text">
                        {{ item.name }}
                    </v-list-item-title>

                    <template v-slot:append>
                        <v-icon size="small" class="arrow-icon">mdi-chevron-right</v-icon>
                    </template>
                </v-list-item>
            </v-list>

            <!-- Footer del Drawer -->
            <template v-slot:append>
                <div class="drawer-footer">
                    <p class="footer-text">🌹 Formando líderes con valores 🌹</p>
                </div>
            </template>
        </v-navigation-drawer>
        <!-- Contenido Principal -->
        <v-main>
            <nuxt />
        </v-main>
    </div>
</template>

<script>
export default {
    name: 'ModernHeader',

    data() {
        return {
            drawer: false,
            scrolled: false,
            navigationItems: [
                {
                    name: 'Inicio',
                    route: '/',
                    icon: 'mdi-home'
                },
                {
                    name: 'Documentación',
                    route: '/documentacion',
                    icon: 'mdi-book-open-variant'
                },
                {
                    name: 'Galería',
                    route: '/galeria',
                    icon: 'mdi-image-multiple'
                },
                {
                    name: 'Programación',
                    route: '/programacion',
                    icon: 'mdi-calendar-clock'
                },
                {
                    name: 'Programas',
                    route: '/programas',
                    icon: 'mdi-radio'
                },
                {
                    name: 'Nuestro Equipo',
                    route: '/creditos',
                    icon: 'mdi-account-group'
                }
            ]
        }
    },

    mounted() {
        // Detectar scroll para efectos visuales
        window.addEventListener('scroll', this.handleScroll)
    },

    beforeUnmount() {
        window.removeEventListener('scroll', this.handleScroll)
    },

    methods: {
        handleScroll() {
            this.scrolled = window.scrollY > 50
        }
    }
}
</script>

<style scoped>
/* App Bar Styles */
.header-bar {
    background: linear-gradient(135deg, #1b5e20 0%, #2e7d32 50%, #4caf50 100%) !important;
    position: relative;
    overflow: hidden;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.header-bar.scrolled {
    background: linear-gradient(135deg, #0d2818 0%, #1b5e20 50%, #2e7d32 100%) !important;
    backdrop-filter: blur(10px);
}

.gradient-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: linear-gradient(45deg, rgba(255, 255, 255, 0.1) 0%, transparent 50%);
    pointer-events: none;
}

/* Wave Effect */
.wave-effect {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 4px;
    background: linear-gradient(90deg, #81c784, #a5d6a7, #c8e6c9);
    animation: wave 3s ease-in-out infinite;
}

@keyframes wave {

    0%,
    100% {
        transform: translateX(-100%);
    }

    50% {
        transform: translateX(100%);
    }
}

/* Logo Section */
.logo-section {
    z-index: 2;
}

.logo-avatar {
    background: linear-gradient(135deg, #fff 0%, #f1f8e9 100%) !important;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
    border: 2px solid rgba(255, 255, 255, 0.3);
}

.logo-emoji {
    font-size: 24px;
    animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {

    0%,
    100% {
        transform: scale(1);
    }

    50% {
        transform: scale(1.1);
    }
}

/* Title Section */
.main-title {
    font-size: 1.8rem;
    font-weight: 700;
    color: white;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    margin: 0;
    line-height: 1.2;
    background: linear-gradient(45deg, #fff, #f1f8e9);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

.institution-subtitle {
    font-size: 0.85rem;
    color: rgba(255, 255, 255, 0.9);
    margin: 0;
    font-weight: 500;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
}

/* Desktop Navigation */
.desktop-nav {
    z-index: 2;
}

.nav-btn {
    color: white !important;
    font-weight: 600;
    border-radius: 25px;
    margin: 0 4px;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
    overflow: hidden;
}

.nav-btn::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
    transition: left 0.5s;
}

.nav-btn:hover::before {
    left: 100%;
}

.nav-btn:hover {
    background: rgba(255, 255, 255, 0.15) !important;
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.2);
}

/* Mobile Drawer */
.mobile-drawer {
    background: linear-gradient(180deg, #1b5e20 0%, #2e7d32 100%);
}

.drawer-header {
    padding: 32px 24px 24px;
    text-align: center;
    background: linear-gradient(135deg, rgba(255, 255, 255, 0.1) 0%, transparent 100%);
}

.drawer-title {
    color: white;
    font-weight: 700;
    margin-bottom: 4px;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
}

.drawer-subtitle {
    color: rgba(255, 255, 255, 0.8);
    font-size: 0.9rem;
    margin: 0;
}

/* Mobile Navigation List */
.mobile-nav-list {
    background: transparent;
    padding: 16px 0;
}

.mobile-nav-item {
    margin: 4px 16px;
    border-radius: 12px;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
    overflow: hidden;
}

.mobile-nav-item::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
    transition: left 0.6s;
}

.mobile-nav-item:hover::before {
    left: 100%;
}

.mobile-nav-item:hover {
    background: rgba(255, 255, 255, 0.1);
    transform: translateX(8px);
}

.nav-icon {
    color: #81c784;
    font-size: 24px;
}

.nav-text {
    color: white;
    font-weight: 600;
    font-size: 1.1rem;
}

.arrow-icon {
    color: rgba(255, 255, 255, 0.6);
    transition: all 0.3s ease;
}

.mobile-nav-item:hover .arrow-icon {
    color: #81c784;
    transform: translateX(4px);
}

/* Drawer Footer */
.drawer-footer {
    padding: 20px;
    text-align: center;
    background: linear-gradient(135deg, rgba(0, 0, 0, 0.1) 0%, transparent 100%);
}

.footer-text {
    color: rgba(255, 255, 255, 0.8);
    font-size: 0.85rem;
    margin: 0;
    font-style: italic;
}

/* Responsive */
@media (max-width: 1280px) {
    .main-title {
        font-size: 1.5rem;
    }

    .institution-subtitle {
        font-size: 0.8rem;
    }
}

@media (max-width: 960px) {
    .main-title {
        font-size: 1.3rem;
    }

    .institution-subtitle {
        display: none;
    }
}

@media (max-width: 600px) {
    .main-title {
        font-size: 1.1rem;
    }
}

/* Animaciones adicionales */
.header-bar {
    animation: slideDown 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

@keyframes slideDown {
    from {
        transform: translateY(-100%);
        opacity: 0;
    }

    to {
        transform: translateY(0);
        opacity: 1;
    }
}

/* Router Link Active States */
.v-btn--active {
    background: rgba(255, 255, 255, 0.2) !important;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.v-list-item--active {
    background: rgba(255, 255, 255, 0.15);
}

.v-list-item--active .nav-icon,
.v-list-item--active .nav-text {
    color: #a5d6a7 !important;
}
.image {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    margin-right: 16px;
}
</style>