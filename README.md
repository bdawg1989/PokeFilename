# PokeFilename
PKHeX-Plugin to customize the PKM output filename

# Latest Changes: 3/10/2024

Thanks to [@ivanlonel](https://github.com/ivanlonel)
Adds the following extensions:

ConditionalGender: prints `♂` if male,`♀` if female and an empty string if `genderless`.

ConditionalStatNature: prints the stat (minted) nature number (padded to 2 digits) only if it's different from original nature, empty string otherwise. The printed string starts with the character `➔`, so you can do `{Nature:00}{ConditionalStatNature}` and get 21➔15.

ConditionalStatNatureName: prints the stat (minted) nature name only if it's different from original nature, empty string otherwise. The printed string starts with the character ➔, so you can do {(Nature)Nature}{ConditionalStatNatureName} and get Gentle➔Modest.

ConditionalScale: prints Scale if available (Legends Arceus or newer), HeightScalar as a second option and an empty string for older saves. Preceded by -  if not empty. Example: `{(Species)Species} {ConditionalScale}` ➔ Wailord - 255.

Alpha and ConditionalAlpha: Like Gigantamax and ConditionalGigantamax, the first prints Alpha if the pokémon is an alpha, and the second prints (Alpha).

ConditionalNickname: prints the nickname in square brackets if the pokémon is nicknamed, empty string otherwise. I know {Nickname} already defaults to the species name if the pokémon isn't nicknamed, but if the pokémon is in a different language it will print the species name in that language, while `{(Species)Species}` always prints it in English. So you can do `{ConditionalNickname} {(Species)Species}` and your Japanese Ditto will still be printed as just Ditto if not nicknamed (or [Masuda] Ditto if its nickname is Masuda).

ConditionalTeraType: prints - Tera <type> only if the pokémon is in a save from a game that supports tera types (currently only SV). Example: `{(Species)Species} {ConditionalTeraType}` ➔ Latios - Tera Electric.

PaddedDisplaySID: prints the DisplaySID padded to 4 digits if the pokémon is from gen 7 or later, 5 digits otherwise.

PaddedDisplayTID: prints the DisplayTID padded to 6 digits if the pokémon is from gen 7 or later, 5 digits otherwise.

Example custom string:
`{Species:0000}{ConditionalForm} {ShinyType} - {ConditionalNickname} {(Species)Species} {ConditionalFormName} {ConditionalGigantamax} {ConditionalAlpha} {ConditionalGender} - {(Nature)Nature}{ConditionalStatNatureName} - {(Ability)Ability} ({AbilityNumber}) {ConditionalTeraType} - {IV_HP:00}.{IV_ATK:00}.{IV_DEF:00}.{IV_SPA:00}.{IV_SPD:00}.{IV_SPE:00} - {(Ball)Ball} {ConditionalScale} - {MetDate.Year}.{MetDate.Month:00}.{MetDate.Day:00} - {OT_Name} ({PaddedDisplaySID}.{PaddedDisplayTID}) - {(GameVersion)Version} - {Checksum:X4}{EncryptionConstant:X8}`

Results obtained using the string above:
`0110-01 ★ - Weezing (Galar) ♀ - Hardy➔Modest - Levitate (1) - Tera Poison - 26.08.31.31.26.31 - Dream - 255 - 2024.01.23 - PKHeX (1234.123456) - SL - 06B4BE74AF7F.pk9`


`0720 - [HoompaLoompa] Hoopa - Modest - Magician (1) - Tera Psychic - 31.31.05.03.09.31 - Cherish - 115 - 2024.01.23 - Mac (00553.11275) - AS - 5FCD2C013F95.pk9`


`0413-01 - Wormadam (Sandy) (Alpha) ♀ - Hasty➔Impish - Anticipation (2) - 22.08.16.31.31.31 - LAPoke - 255 - 2024.01.23 - PKHeX (1234.123456) - PLA - 754A248533DD.pa8`


`0892-01 - Urshifu (Rapid-Strike) (Gigantamax) ♂ - Jolly - UnseenFist (2) - 00.31.00.31.00.31 - Poke - 70 - 2024.01.23 - PKHeX (1234.123456) - SW - 99430A33EE61.pk8`


`0029 ■ - [Juliet] NidoranF ♀ - Brave➔Timid - Hustle (4) - 20.07.14.28.05.19 - Poke - 158 - 2024.01.23 - PKHeX (1234.123456) - SH - 58CA90D44919.pk8`


`0025-01 - Pikachu (Original) ♂ - Hardy - Static (1) - 00.22.23.12.11.22 - Poke - 2024.01.23 - Ash (0275.090898) - SN - B23C8BFA260E.pk7`


`0385 - [StarFace] Jirachi - Hardy - SereneGrace (1) - 26.31.31.31.04.23 - Cherish - 2024.01.23 - GF (00559.04016) - Y - E949B67FD26A.pk7`


`0669-03 - [Egg] Flabébé (Blue) ♀ - Naive - FlowerVeil (2) - 13.02.29.13.22.11 - Luxury - 2017.02.23 - PKHeX (54321.12345) - X - 5F7E1F08A3E9.pk6`


# About  
This project uses `PKHeX.Core` and PKHeX's `IPlugin` interface to customize the file name of exported PKM files. Please refer to the [Wiki](https://github.com/architdate/PokeFilename/wiki) for more information regarding the functionalities provided by this project.

This project is owned by [@architdate](https://github.com/architdate) (Discord: thecommondude)

## CI/CD Builds
This project has Azure CI/CD setup to auto build commits on every commit. People who are not keen on building the project themselves, may use the CI/CD to download the built plugin.

## Building  
This project requires an IDE that supports compiling .NET based code (.NET 8.0). Recommended IDE is Visual Studio 2022.

**Regular Builds**  
Regular builds will usually succeed unless there are changes that are incompatible with the NuGet [PKHeX.Core](https://www.nuget.org/packages/PKHeX.Core) package dependency specified in the `.csproj` files of the projects.

- Clone the PokeFilename repository using: `$ git clone https://github.com/architdate/PokeFilename.git`.
- Right-click on the solution and click `Rebuild All`.
- These DLLs should be placed into a `plugins` directory where the PKHeX executable is. You may also combine these DLL files using ILMerge.
   - The compiled DLLs for PokeFilename will be in the `PokeFilename.GUI/bin/Release/net8.0-windows` directory:
     * PokeFilename.GUI.dll
     * PokeFilename.API.dll

## Usage  
To use the plugins:
- Create a folder named `plugins` in the same directory as PKHeX.exe.
- Put the compiled plugins from this project in the `plugins` folder. 
- Start PKHeX.exe.
- The plugins should be available for use in `Tools > PokeFilename` drop-down menu.

## Support Server
Come join the dedicated Discord server for this mod! Ask questions, give suggestions, get help, or just hang out. Don't be shy, we don't bite:
To unlock the help channel, use `!unlock hammerhead` in the `bot-testing` channel.

[<img src="https://canary.discordapp.com/api/guilds/401014193211441153/widget.png?style=banner2">](https://discord.gg/tDMvSRv)

## Contributing

To contribute to the repository, you can submit a pull request to the repository. Try to follow a format similar to the current codebase. All contributions are greatly appreciated! If you would like to discuss possible contributions without using GitHub, please contact us on the support server above.

## Credits
**Repository Owners**
- [architdate (thecommondude)](https://github.com/architdate)

**Namer Credits**

| Namer | Author |
| --- | --- |
| [@architdate](https://github.com/architdate) | Creator of CustomNamer Template |
| [@Lusamine](https://github.com/Lusamine) | Creator of AnubisNamer Template |

Feel free to contribute complex Namer templates by opening a Pull Request through GitHub issues!

**Credit must be given where due...**

- [FlatIcon](https://www.flaticon.com/) for their icons. Author credits (Vitaly Gorbachev).
