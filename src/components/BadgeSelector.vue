<template>
    <div>
        <img v-for="badge in badges" :key="badge" :src="require('@/assets/badges/'+badge)" />
    </div>
</template>

<script>
export default {
    data: ()=>({
        badges: ["Akame ga kill_badge.png","Alice in Borderland_badge.png","Angel Beats_badge.png","Assassination Classroom_badge.png","Attack on Titan_badge.png","Bakemonogatari_badge.png","Berserk_badge.png","BlazBlue_badge.png","Bleach_badge.png","Blue Exorcist_badge.png","Bungou Stray Dogs_badge.png","Castlevania_badge.png","Chainsaw man_badge.png","Chivalry Of a Failed Knight_badge.png","Clannad_badge.png","Darling in the FranXX_badge.png","Darwins Game_badge.png","Death Note_badge.png","Demon Slayer_badge.png","Devil May Cry_badge.png","Dragon Ball_badge.png","Erased_badge.png","Fate_badge.png","Final Fantasy_badge.png","Fire Force_badge.png","Fullmetal Alchemist_badge.png","Genshin Impact_badge.png","Great Pretender_badge.png","High school of the Dead_badge.png","How a Realist Hero Rebuilt the Kingdom Part 2_badge.png","Hunter x Hunter (2011)_badge.png","Hunter x Hunter_badge.png","Identity V_badge.png","Interviews with Monster Girls_badge.png","Jojo Bizarre Adventure_badge.png","Jujutsu Kaisen_badge.png","Kaguya-sama Love is War_badge.png","Kakegurui_badge.png","Kingdom Hearts_badge.png","Konosuba_badge.png","My Hero Academia_badge.png","Naruto_badge.png","Neon Genesis Evangelion_badge.png","Nichijou_badge.png","Non Non Biyori_badge.png","Noragami_badge.png","Oreshura_badge.png","Overlord_badge.png","Persona_badge.png","Pokemon Trainers_badge.png","Promised Neverland_badge.png","RWBY_badge.png","Rascal Does Not Dream of Bunny Girl Senpai_badge.png","Rent-a-Girlfriend_badge.png","STEINS GATE_badge.png","Soul Eater_badge.png","Sword Art Online _badge.png","Sword Art Online_badge.png","That Time I Got Reincarnated as a Slime_badge.png","Vinland Saga_badge.png","Yuru Camp_badge.png","booster.png","missing.png","mob psycho 100_badge.png","ouran highschool host club_badge.png","tier1-patreon.png","tier2-patreon.png","tier3-patreon.png","violet evergarden_badge.png"],

    })
}
</script>