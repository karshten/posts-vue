<template>
    <main class="posts">
        <PostForm
            :posts="posts"
            @createPost="createPost"
        />
        <PostList :posts="posts"/>
    </main>
</template>

<script>
    import PostList from "./components/PostList";
    import PostForm from './components/PostForm'
    export default {
        components: {PostForm, PostList},
        data() {
            return {
                posts: [
                    {
                        id: 1, title: 'Vue',
                        img: "icons8-vue-js-480.svg",
                        description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Beatae, cumque cupiditaLorem ipsum dolor sit amet, consectetur adipisicing elit. Beatae, cumque cupiditaLorem ipsum dolor sit amet, consectetur adipisicing elit. Beatae, cumque cupidita'
                    },
                    {
                        id: 2, title: 'React',
                        img: "data:image/png;base64,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",
                        description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Beatae, cumque cupidita'
                    },
                    {
                        id: 3, title: 'Angular',
                        img: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAzFBMVEX////DAC/dADHQADDBACXcACfCACvCACjdAC3dAC/AABrBACDcACW+AADDACTocoLXcoHbABvcACHbABXgMUzIMUrtxsy/ABH13eHbAA7cAB/78fPmrLTdj5q/AAjbABftmqTptr3wq7TNSl7GFjrfIELkWWzvo6z419vaAAD75unjS2DqhJHpeYjytLzag47hO1PmYnTkpK3skZ3ZeYbJLEfPU2XhmqT1xMvqgY7PAB387vH30NXVaXjGEjfeFDvKAADcipXLPVTSXG1tpM47AAALT0lEQVR4nO2da1faTBSFwy3ctYAttxaoVgRFWl9rS6utvfz///RmEqKBc2YyM+dApGuejy5XZAvsPWcnk3iew+FwOBwOh8PhcDgcDofD4XA4HA4HwsP19x9vsn4Ru6N3+9hpFIrd8sdZ1i9lF9xfnPTblXy+kMv5R90PXy+zfkG8DJdXcyEvHyoM8OvNP/8Ns35ZbKxuOoNI3pPCUOToy/usXxoHD9ftcamazwOFAeVa7dB9p3db7TQS8rYUBhS79cP1nfvJSX9LHlR4wL5zetVvV7blYQqjr+TrA/Od1U1/gMmTKIzM9XB8J/CWVgmXJ1cY+k73EHynd5vf9hZdhYfgO/eTc8RbDBSGvpN790J9ZyjzFiOFse/cZy0HsJp2ZN5iqjASefaifOfheNwqpXw6jRTmhO80X4rvzBb5jq48A4U54TtHnzP3nUsNb7FWGPrOz3e97OQNTz/peAtBYS78St5ltN55P5WuW1R8N1QYimzu33cejgfa3rJBa1kzl7j39c5sUTLxliSVK++sbCMx8J1abT++Y+4tSTor703XTmHAHnzHyluSb+FjcJAPvrXEXa93ltO5jbckaJ0Gh3lr9U1MiGyevd2Fub45bilmIj2qpfBQdcKbGBL4zl9m35ktKrbekqR9Gx7tXZ2oMBf5zgOXvMvJI8Fbkm9hJ/pwDe29ZkNk1//N4DtUb0lSOl4f9FWRRWK43vlK852l7kykxTz+j/eaPAojkWdv7QXO5nzywrSPsU19lHLTfiEw7DAKzHee7Y+Q+ggjQnawGMyaynniwJTUB9TtBXrnjJ/S1jJxYGLqb+D/JCic8ilcp30MOfWfKX8hKLxusClcp30MR+qvKf4gKJy0uQRW+5t2MOQLjPpXgsLlgEth43rr0Fypn8vVCHnoPYy5FPa3e2y+1K9RFuGXXIFYmYJjs6V+l3QSoM+ksAPnALbUpwS+5w14Ir9yghybK/VHFIHeJ55A3Ej7GKbU91+TFN5Qx/qQrbSP4VFICnzPW7BEfnuCHpwn9Y8+khRecARidYx7wXDEoZAU+J73vsWgEKR9DEvq12iF/4wjEEHax/Q43sQurQi/ZwjEEkz7GI7UpwW+543pgdiXt34cqU+LQ897JAcimvYx9NQnzb+CK7JCNO1j6KlPDHzPOyY3+Xnl8cmzPmn+FdxSZ+DBRHl8cuoTA9/zTomRXx2rj09u+Ov/ERWuiJHf+JbyB6ipT5p/BT1i5M/T0oo66xMDn1x7K9I+hpj6tPlXQKu9Ydqfbv+AmPqUwjuCVHtXPm0fbvgL/M9JqU8OfGLtPQbr/skvMOyQUp84/wootXcFpn2+kAM/o6R+8RVZIaX2HlxsH201LnSBvVNSnzj/Cgi1d7UDjnZVKsDPFaXhJxXeEYTau7HYPthlP/iUjkBEElKfHPik2hvO9otGoBCuJAmpT51/BdZTfukGHKtdDRT6MMLsU58e+ITauw/WU8tWeAUt7I7sU5864Qtsa2+Y9t7Jeg8pHFptU588/wpsa+/xavtIM/GBF1dBj8C7a5v6DIFvXXsjaR/2BUIhEtOWCsnzr8Cy9oZpP+xU1wpzXeAPlqnPEPi2tXd1AA40Cf9VBfyFWTb8xMI7wq72hmm/LiZDhchEYJf65PlXYFd798Elg6voPxXtt4CLU7uGnyPw7WpvJO2nyf34iAdapT5HHNrV3jDt7+f5hMJcE7zHNqnvw1HMBovaG0n7OHTWCuu/wW9YpD5L4FvV3h2Q9k99z1ohsji1SH1y4R1hXnuH2yo2WcaZE+/sQnzefNZnCXyb2nsACrXn1W2s0P8Dfsc89cmFd4Rx7V1tg2PMniLnaXfeCFxnb97wM8y/AuPae+tCS8Hzd/lJIbI4NU59lsC3qL3ncINA/ylTn3dYwiwznvU55l+BYe39tK3imcTq/Vkh8iUyTX164R1hWHvDtE8uGp4V+h/A7xmmPkPhHWFWeye2VcSsEp/zxD5guDg1TH2W+VdgVnsjaT9NrBkSCst/wW+apT5T4BvW3hvbKiI2ppPkXu4RtKQjkzeRZf4VGNXeSNpvLIqSCuvvwO8apT5D4R1hUnsjs71oSXGFyOLUqOFnCnyz2htJ++XGmmjjjgPI4tQk9XnmX4H+lL+9rUKwWbhuKCzDxalJ6nMFvkntjaT9bF5JUvCTNOEmUIPU55nwBfq1dx++4sX5SZK710nu4Pijn/pM869Au/ZG0t4c7dRnC3yD2htJe3O0U59p/hXo1t5I2tugq5At8PVr7xZMext0U5+l8I7QrL0l2yqM0W34meZfgWbtjaS9HZqpzxf4ntfRCcT4lgl0NBt+vjjUrL0bMO1t0Up9psI7Qqv2RtLeFq3UZwx8vdqbJe1jdFKfbf4V6NTeyCZKe3RSnzHwtWpvprSP0Wj4mQrvCI3aW7mtwhyN1GebfwXptTdX2sdoNPyMga9Te0s2UdqTnvp8868gtfZGZnsa6bN+jfXvpdXe2CbKVqOE8P0IoQ7bjNTUZyu8I9Jqb2QT5XJcxcDvfYm0GWmpzzj/ClJqb+SWCbJ1EK4Qy7aU1GcN/NTaG0n7S8k8Irl/KfKlSkl9xvlXoK69sU2UsuZDphCZZtUNP1vhHaGuvbG0l7mvRCHSnKakPmvgp9TeWNovZasg2V124Wn9lIafc/4VqKZ8LO2lFatMIeY1ytTnDXxl7Y3N9jKfUdwpuQv/qDL1OSd8gaL2xtJe3rBKFWJeo0h91vlXoKi9sVsmyFd5UoXIJUSq1GcOfNWbgm2ilPqM6n7eiNcoUp91/hXIa2/slgmKXkeuEHvN8tRnDnxF7Y2lvdxnlPdkx4YFqULGwjtiJot8LO1VZ3JUCpEXLU191vlXIKu90VsmtBTTpEIhZo/Shp878KW1N3bLBIXPqJ8cgHmNLPW541BWe6O3TFCeMlYpxLxG0vCzFt4RuD1it0zoKc/jKJ/+gHkNnvrsgS+rvZELLb1vymlZrRDxGjz1medfAVp7o7dMaCtbK6VCbF2Dpz574Etqb+RCS7XPpD2jBPMaNPVZC+8IrPZGtlWkXpqiVnj0GTki1vAzz78C7Ez3GEl7tc+kPmcGmaHQ1GcPfLT2RjZRpvlMqkKsfcEafu75VwAHojZ26YXaZ9Kfu4Z5zWeY+ryFdwSsvUvHkGnaudS0pyEd/XgF+AsicQeBj9beSGmfejo89XlPRQjMfPb5V8B0b2/TJ1pJ/g38gR8EIs+DElgUlpv8cRjQu+ozaGRQ6Hf/7OrBT6tz+o0i6QprPzmugJRxWqLeHZqqsF7byQc0we2Y5jg0hcUR3F3LzvCY9HWkKCw3f+zn+aQky7FXGBjM/h72+HBibTm2Cv3ah/0+lnRZtbQcS4X1HQyEadx2rCzHSmGxuQeDgQyv+xY357FQGBhMVg9ev5yaW46xQn90luHTZIXlGGo0VLh3g4Es82aWY6awXuS94sKOScvEckwUHnXhFsxMGH6b61uOvsJy81VWBgMxsBxdhRkbDOThpKOnUU+h373L2mAgmpajpfBlGAxkMtC4pF9D4YsxGMjwW/oqJ1XhizIYSLrlpDXCoy/sp6+ZmX1SW4767Fr3jnNfyq5YPVpeqZCr+dyXkOyKi5b87IXiiqER90VAu2QhtRyZwuLo80s2GMj9jcRycIX+6O9LNxiIxHIwhX739SEYDAS1HERhLXcoBgO5aIBVDlBYrx2SwUAW24PVlsJi8+NhGQxk23I2FAYGs58Se7fMNiryhMLAYHZ1lmzfJC3nSaF/yAYDOS21N+9fevAGA4kr8sJ6BcN/XVrm3B+HFwIIheXmP2EwkPCsXGGXp+GzZ3U+Luz2NHz2nBb2f5bM4XA4HA6Hw+FwOBwOx7/A/0fFGxADXZ4GAAAAAElFTkSuQmCC",
                        description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Beatae, cumque cupidita'
                    },
                    {
                        id: 4, title: 'Vue',
                        img: "icons8-vue-js-480.svg",
                        description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Beatae, cumque cupidita'
                    },
                ],
            }
        },
        methods: {
            createPost(newPost) {
                this.posts.push(newPost)
            }
        }
    }
</script>
<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    body {
        font: 16px sans-serif;
        margin: 0;
        padding: 0;
    }

    .posts {
        padding: 20px;
        max-width: 1200px;
        margin: 0 auto;
    }
</style>